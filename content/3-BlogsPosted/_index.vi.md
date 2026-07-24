---
title: "Các bài blogs đã đăng"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Các bài blog đã đăng

Trong quá trình thực tập FCAJ, mình đã viết và đăng **3 bài blog** lên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) — tập trung vào các dịch vụ serverless và event-driven trên AWS mà mình học được khi xây dựng dự án InsightShare.

Các bài viết chia sẻ góc nhìn thực tế: từ những hiểu lầm ban đầu, cách từng service giải quyết vấn đề cụ thể, đến khi nào nên dùng và best practices cơ bản.

#### Danh sách bài viết

| STT | Bài viết | Chủ đề |
| --- | --- | --- |
| 1 | [Amazon SQS: Hàng đợi tin nhắn giúp hệ thống AWS không bị "nghẽn"](3.1-Blog1/) | Message queue, xử lý bất đồng bộ |
| 2 | [AWS Step Functions: Điều phối workflow nhiều bước mà không viết code phức tạp](3.2-Blog2/) | Workflow orchestration |
| 3 | [Amazon API Gateway: Cổng vào cho ứng dụng serverless trên AWS](3.3-Blog3/) | API management, HTTP/HTTPS |

#### Tóm tắt từng bài

**[Blog 1 – Amazon SQS](3.1-Blog1/)**  
Giới thiệu Amazon SQS — dịch vụ hàng đợi tin nhắn serverless giúp tách producer và consumer, xử lý bất đồng bộ và hấp thụ traffic spike mà không cần tự host message queue trên EC2. Bài viết so sánh Standard vs FIFO queue, giải thích vì sao không nên gọi thẳng Lambda/API, và use case xử lý đơn hàng e-commerce.

**[Blog 2 – AWS Step Functions](3.2-Blog2/)**  
Giới thiệu AWS Step Functions — dịch vụ điều phối workflow serverless giúp gom nhiều bước xử lý (validate → xử lý → gửi email → cập nhật DB) thành luồng rõ ràng, có retry và xử lý lỗi sẵn mà không cần viết code Lambda phức tạp.

**[Blog 3 – Amazon API Gateway](3.3-Blog3/)**  
Giới thiệu Amazon API Gateway — dịch vụ quản lý API fully managed giúp expose Lambda và các backend AWS ra internet qua HTTP/HTTPS, có sẵn throttling, auth và CORS mà không cần quản lý server hay cấu hình Nginx.

#### Mối liên hệ với dự án InsightShare

Ba dịch vụ trên đều xuất hiện trong kiến trúc serverless của dự án **InsightShare**:

```
Client → API Gateway → Lambda → S3 / DynamoDB
                    → SQS (xử lý bất đồng bộ)
                    → Step Functions (workflow phức tạp)
```

API Gateway là cổng vào cho frontend gọi API; SQS hấp thụ tải khi có nhiều request upload/analyze đồng thời; Step Functions phù hợp khi cần điều phối nhiều bước xử lý AI sau khi file được tải lên.
