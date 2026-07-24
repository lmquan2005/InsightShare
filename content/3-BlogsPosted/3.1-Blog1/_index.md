---
title: "Blog 1"
date: 2026-07-24
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON SQS: MESSAGE QUEUES THAT KEEP AWS SYSTEMS FROM BOTTLENECKING

Amazon SQS (Simple Queue Service) is a fully managed, serverless message queue on AWS. Components send and receive messages asynchronously without direct coupling. Instead of Service A calling Service B directly, the flow is Service A → SQS → Service B — reducing coupling, absorbing traffic spikes and eliminating the need to self-host RabbitMQ/Redis on EC2.

Key points to know:

* **Two queue types:** Standard (high throughput, at-least-once delivery) suits email/logs/analytics; FIFO (strict ordering, exactly-once processing) suits payments and order processing.
* **Important concepts:** Dead Letter Queue (DLQ) holds failed messages after retries; Visibility Timeout hides a message while it is being processed; Long Polling reduces empty API calls.
* **Why not call Lambda/API directly:** users wait for heavy processing (timeouts are common); traffic spikes overload downstream services; manual retries make code complex and hard to debug.
* **How SQS helps:** the producer only enqueues a message and responds quickly; consumers (Lambda, EC2, ECS…) process when ready and scale with message volume; messages are not lost when a consumer is temporarily down.
* **E-commerce use case:** the API accepts an order → saves to DynamoDB → pushes to SQS → returns 201 immediately; a Lambda consumer sends email, updates inventory and syncs CRM in the background.
* **Common integrations:** Lambda event source mapping, SNS fan-out → SQS, EventBridge routing, EC2/ECS worker polling, Step Functions.
* **Best practices:** always attach a DLQ; write idempotent consumers (at-least-once); set VisibilityTimeout to match real processing time; use long polling; monitor CloudWatch (`ApproximateNumberOfMessagesVisible`, `AgeOfOldestMessage`).
* **Cost:** free tier of 1 million requests/month; Standard ~$0.40 per million requests; no queue maintenance fee within the same region.

SQS is a foundational buffer for event-driven architectures on AWS. If you are new to serverless, try a simple flow: API Gateway → Lambda (producer) → SQS → Lambda (consumer) to see the difference between synchronous and asynchronous processing.

**References:**

* [Amazon SQS – AWS Documentation](https://docs.aws.amazon.com/sqs/)
* [SQS Best Practices – AWS Documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-best-practices.html)
* [How AutoScout24 built a Bot Factory with Amazon Bedrock](https://aws.amazon.com/blogs/)
