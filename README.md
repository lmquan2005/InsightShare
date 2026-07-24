# InsightShare

A serverless document assistant on AWS, built as the capstone for the **First Cloud AI Journey (FCAJ)** internship at **AWS Vietnam**.

## What it does

You upload an image or PDF, and InsightShare turns it into something you can search and question:

- Extracts text with **Amazon Textract** and detects labels with **Amazon Rekognition**.
- Stores the extracted metadata (text, labels, file info) in **DynamoDB**.
- Lets you search across your files by their actual content, not just filenames.
- Lets you ask questions about a document in plain language, answered by **Amazon Bedrock (Claude)**.

The original files stay in a **private S3 bucket**. The browser never gets public URLs; it uploads and downloads through short-lived **presigned URLs**.

## How it works

End-to-end flow:

1. The frontend (static site on **Cloudflare Workers**, mirrored on **GitHub Pages**) calls **API Gateway**.
2. API Gateway routes to **Python Lambda** functions.
3. **Upload:** Lambda returns a presigned S3 URL and the browser puts the file straight into the private bucket.
4. **Analyze:** a Lambda runs Textract and Rekognition on the file, then writes the text and labels to DynamoDB.
5. **Search:** a Lambda queries the stored text and labels and returns matching files.
6. **Ask:** a Lambda sends your question to Bedrock (Claude) with the document's stored text as context, and returns the answer.

```
Browser (Cloudflare Workers / GitHub Pages)
        │
        ▼
  API Gateway (HTTP API)
        │
        ▼
  Lambda (Python)
   ├── S3          (private files, presigned URLs)
   ├── DynamoDB    (metadata, text, labels)
   ├── Textract    (OCR)
   ├── Rekognition (image labels)
   └── Bedrock     (Claude — Q&A, Vietnamese)
```

## Design notes

| Topic | Detail |
| --- | --- |
| **Region** | `ap-southeast-1` (Singapore) |
| **Cost** | ~$1/month at demo scale — pay-per-use, idle cost near zero |
| **IAM** | Least-privilege roles, one per function, scoped to the resources it touches |
| **Monitoring** | CloudWatch logs and metrics across the Lambdas and API |

## AWS services used

| Service | Role |
| --- | --- |
| Amazon S3 | Private file storage + static frontend hosting |
| Amazon API Gateway | Public HTTP API entry point |
| AWS Lambda | Business logic (Python) |
| Amazon DynamoDB | File metadata, extracted text and AI labels |
| Amazon Textract | Document text extraction |
| Amazon Rekognition | Image label detection |
| Amazon Bedrock (Claude) | Document Q&A and summarization |
| Amazon CloudFront | HTTPS delivery (optional) |
| Amazon CloudWatch | Logs, metrics and alarms |
| AWS IAM | Least-privilege access control |

## Internship report (this repo)

This repository also contains the full **FCAJ internship report** — a bilingual Hugo site with:

- Weekly worklog (8 weeks)
- Project proposal
- AWS blog posts (SQS, Step Functions, API Gateway)
- Hands-on workshop guide
- Self-evaluation

### Run the report site locally

```bash
hugo server
```

Open `http://localhost:1313` (English) or `http://localhost:1313/vi/` (Vietnamese).

### Build for production

```bash
hugo --minify
```

Output is written to `public/`. GitHub Actions deploys automatically to **GitHub Pages** on push to `main`.

## Author

**Lại Minh Quân** — AWS062026, FCAJ Workforce Bootcamp, AWS Vietnam

## License

Internship capstone project. Content and architecture documentation for educational purposes.
