---
title: "Thêm AI: Rekognition, Textract, Bedrock (Claude)"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5.4.5 </b> "
---

#### Mục tiêu

Tích hợp **lớp AI** vào Lambda function để InsightShare gắn nhãn ảnh, trích văn bản tài liệu và trả lời câu hỏi bằng tiếng Việt. Ba dịch vụ AWS gọi sẵn được dùng — không cần huấn luyện mô hình:

+ **Amazon Rekognition** (`DetectLabels`) — gắn nhãn ảnh
+ **Amazon Textract** (`DetectDocumentText`) — OCR cho PDF và ảnh chữ
+ **Amazon Bedrock** (`InvokeModel`, Claude Haiku) — hỏi đáp và tóm tắt tài liệu bằng tiếng Việt

Kết quả được lưu vào DynamoDB (`labels`, `text`, `search_blob`) để route tìm kiếm có thể tìm file theo nội dung.

#### Route `analyze`

Sau khi trình duyệt upload file lên S3, frontend gọi `POST /files/{id}/analyze`. Lambda đọc object từ S3, chạy đúng dịch vụ AI theo content type, rồi cập nhật dòng DynamoDB:

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

Với ảnh, Rekognition trả về nhãn như `Diagram`, `Architecture`, `Text`. Với PDF và ảnh chữ, Textract trích văn bản hiển thị. File `.txt` thuần được đọc trực tiếp từ S3.

#### Route `ask` (Bedrock / Claude)

`POST /files/{id}/ask` gửi văn bản đã lưu tới **Amazon Bedrock** (Claude Haiku) và trả về câu trả lời tiếng Việt. Câu hỏi rỗng sẽ kích hoạt tóm tắt:

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
**Quyền truy cập Bedrock.** Luồng code đã được nối đầy đủ. Trên tài khoản dạng credit chưa có inference quota on-demand của Bedrock, `InvokeModel` có thể bị giới hạn — handler có thể trả về câu dự phòng ở HTTP 200 cho tới khi được cấp quota. Bật quyền truy cập model Claude Haiku trong console Bedrock (region `ap-southeast-1`) trước khi test.
{{% /notice %}}

#### Tìm kiếm theo nội dung

Trường `search_blob` (nhãn + văn bản viết thường) được ghi trong `analyze`. Route tìm kiếm scan DynamoDB và lọc các item có `search_blob` chứa từ khóa:

```python
def search_files(event):
    q = event.get("queryStringParameters", {}).get("q", "").lower()
    items = table.scan().get("Items", [])
    hits = [i for i in items if q in i.get("search_blob", "")]
    return _resp(200, hits)
```

Nhờ đó người dùng tìm được sơ đồ kiến trúc bằng cách gõ `diagram` dù tên file là `IMG_0042.jpg`.

#### Test lớp AI

```bash
API="https://<api-id>.execute-api.ap-southeast-1.amazonaws.com"

# Upload ảnh, rồi analyze
curl -X POST "$API/files/<id>/analyze"
# → {"labels": ["Diagram", "Architecture", "Text"], ...}

# Tìm theo nhãn AI, không theo tên file
curl "$API/files/search?q=diagram"

# Đặt câu hỏi bằng tiếng Việt
curl -X POST "$API/files/<id>/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "Tài liệu này nói về gì?"}'
```

Sau khi deploy Lambda đã cập nhật, toàn bộ luồng AI chạy đầu-cuối: upload → analyze (Rekognition/Textract) → tìm kiếm theo nội dung → ask (Bedrock/Claude bằng tiếng Việt).

#### Tóm tắt

Lớp AI biến InsightShare từ lưu trữ file thuần thành nền tảng hiểu nội dung. Rekognition và Textract chạy tự động sau upload; Bedrock trả lời câu hỏi trên văn bản đã trích — tất cả qua cùng một Lambda function, kết quả được index trong DynamoDB để tìm kiếm thông minh.
