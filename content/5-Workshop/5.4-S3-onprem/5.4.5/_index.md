---
title: "Add AI: Rekognition, Textract, Bedrock (Claude)"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5.4.5 </b> "
---

#### Goal

Wire the **AI layer** into the Lambda function so InsightShare can label images, extract document text and answer questions in Vietnamese. Three ready-to-call AWS services are used — no model training:

+ **Amazon Rekognition** (`DetectLabels`) — image labels
+ **Amazon Textract** (`DetectDocumentText`) — OCR for PDFs and scanned images
+ **Amazon Bedrock** (`InvokeModel`, Claude Haiku) — Vietnamese Q&A and document summary

Results are saved into DynamoDB (`labels`, `text`, `search_blob`) so the search route can find files by content.

#### The `analyze` route

After the browser uploads a file to S3, the frontend calls `POST /files/{id}/analyze`. Lambda reads the object from S3, runs the right AI service by content type, then updates the DynamoDB row:

```python
rekognition = boto3.client("rekognition", region_name="ap-southeast-1")
textract = boto3.client("textract", region_name="ap-southeast-1")

def analyze(event, file_id):
    item = table.get_item(Key={"id": file_id})["Item"]
    key = item["s3_key"]
    content_type = item.get("content_type", "")

    labels, text = [], ""
    if content_type.startswith("image/"):
        resp = rekognition.detect_labels(
            Image={"S3Object": {"Bucket": BUCKET, "Name": key}},
            MaxLabels=10, MinConfidence=70,
        )
        labels = [l["Name"] for l in resp.get("Labels", [])]
    elif content_type == "application/pdf":
        resp = textract.detect_document_text(
            Document={"S3Object": {"Bucket": BUCKET, "Name": key}}
        )
        text = " ".join(
            b["Text"] for b in resp.get("Blocks", []) if b["BlockType"] == "LINE"
        )
    elif content_type == "text/plain":
        obj = s3.get_object(Bucket=BUCKET, Key=key)
        text = obj["Body"].read().decode("utf-8", errors="replace")

    head = s3.head_object(Bucket=BUCKET, Key=key)
    table.update_item(
        Key={"id": file_id},
        UpdateExpression="SET labels=:l, #t=:t, search_blob=:s, #sz=:sz",
        ExpressionAttributeNames={"#t": "text", "#sz": "size"},
        ExpressionAttributeValues={
            ":l": labels, ":t": text,
            ":s": (" ".join(labels) + " " + text).lower(),
            ":sz": head["ContentLength"],
        },
    )
    return _resp(200, {"id": file_id, "labels": labels, "text": text[:500]})
```

For images, Rekognition returns labels such as `Diagram`, `Architecture`, `Text`. For PDFs and scanned images, Textract extracts the visible text. Plain `.txt` files are read directly from S3.

#### The `ask` route (Bedrock / Claude)

`POST /files/{id}/ask` sends the stored text to **Amazon Bedrock** (Claude Haiku) and returns a Vietnamese answer. An empty question triggers a summary instead:

```python
bedrock = boto3.client("bedrock-runtime", region_name="ap-southeast-1")
MODEL_ID = "anthropic.claude-3-haiku-20240307-v1:0"

def ask_document(event, file_id):
    body = json.loads(event.get("body") or "{}")
    question = body.get("question", "").strip()
    item = table.get_item(Key={"id": file_id})["Item"]
    text = item.get("text", "")
    if not text:
        return _resp(400, {"error": "no text extracted yet — run analyze first"})

    prompt = (
        f"Bạn là trợ lý InsightShare. Trả lời bằng tiếng Việt.\n"
        f"Tài liệu ({item['filename']}):\n{text[:8000]}\n\n"
        f"Câu hỏi: {question or 'Tóm tắt tài liệu này.'}"
    )
    resp = bedrock.invoke_model(
        modelId=MODEL_ID,
        body=json.dumps({
            "anthropic_version": "bedrock-2023-05-31",
            "max_tokens": 1024,
            "messages": [{"role": "user", "content": prompt}],
        }),
    )
    answer = json.loads(resp["body"].read())["content"][0]["text"]
    return _resp(200, {"id": file_id, "answer": answer})
```

{{% notice info %}}
**Bedrock access.** The code path is fully wired. On credit-based accounts without on-demand Bedrock inference quota, `InvokeModel` may be throttled — the handler can return a graceful fallback message at HTTP 200 until quota is granted. Enable model access for Claude Haiku in the Bedrock console (region `ap-southeast-1`) before testing.
{{% /notice %}}

#### Content-based search

The `search_blob` field (lowercase labels + extracted text) is written during `analyze`. The search route scans DynamoDB and filters items whose `search_blob` contains the query:

```python
def search_files(event):
    q = event.get("queryStringParameters", {}).get("q", "").lower()
    items = table.scan().get("Items", [])
    hits = [i for i in items if q in i.get("search_blob", "")]
    return _resp(200, hits)
```

This lets users find an architecture diagram by searching `diagram` even when the filename is `IMG_0042.jpg`.

#### Test the AI layer

```bash
API="https://<api-id>.execute-api.ap-southeast-1.amazonaws.com"

# Upload an image, then analyze it
curl -X POST "$API/files/<id>/analyze"
# → {"labels": ["Diagram", "Architecture", "Text"], ...}

# Search by AI label, not filename
curl "$API/files/search?q=diagram"

# Ask a question in Vietnamese
curl -X POST "$API/files/<id>/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "Tài liệu này nói về gì?"}'
```

After deploying the updated Lambda, the full AI flow works end-to-end: upload → analyze (Rekognition/Textract) → search by content → ask (Bedrock/Claude in Vietnamese).

#### Summary

The AI layer turns InsightShare from plain file storage into a content-aware platform. Rekognition and Textract run automatically after upload; Bedrock answers questions over the extracted text — all through the same Lambda function, with results indexed in DynamoDB for smart search.
