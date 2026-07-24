---
title: "Blogs Posted"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Blogs Posted

During the FCAJ internship, I wrote and published **3 blog posts** to [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) — focusing on serverless and event-driven AWS services I learned while building the InsightShare project.

The posts share a practical perspective: from initial misconceptions, how each service solves a specific problem, to when to use it and basic best practices.

#### Article List

| No. | Article | Topic |
| --- | --- | --- |
| 1 | [Amazon SQS: Message queues that keep AWS systems from bottlenecking](3.1-Blog1/) | Message queue, async processing |
| 2 | [AWS Step Functions: Orchestrate multi-step workflows without complex code](3.2-Blog2/) | Workflow orchestration |
| 3 | [Amazon API Gateway: The entry point for serverless apps on AWS](3.3-Blog3/) | API management, HTTP/HTTPS |

#### Summary of Each Post

**[Blog 1 – Amazon SQS](3.1-Blog1/)**  
Introduces Amazon SQS — a serverless message queue that decouples producers and consumers, enables asynchronous processing and absorbs traffic spikes without self-hosting a message broker on EC2. Covers Standard vs FIFO queues, why not to call Lambda/API directly, and an e-commerce order processing use case.

**[Blog 2 – AWS Step Functions](3.2-Blog2/)**  
Introduces AWS Step Functions — a serverless workflow orchestration service that chains multi-step processing (validate → process → send email → update DB) into a clear flow with built-in retry and error handling, without writing complex Lambda code.

**[Blog 3 – Amazon API Gateway](3.3-Blog3/)**  
Introduces Amazon API Gateway — a fully managed API service that exposes Lambda and other AWS backends over HTTP/HTTPS with built-in throttling, auth and CORS, without managing servers or configuring Nginx.

#### Connection to the InsightShare Project

All three services appear in the **InsightShare** serverless architecture:

```
Client → API Gateway → Lambda → S3 / DynamoDB
                    → SQS (async processing)
                    → Step Functions (complex workflows)
```

API Gateway is the entry point for the frontend; SQS absorbs load during upload/analyze spikes; Step Functions fits when orchestrating multi-step AI processing after a file is uploaded.
