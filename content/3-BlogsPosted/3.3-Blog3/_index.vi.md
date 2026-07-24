---
title: "Blog 3"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AMAZON API GATEWAY: CỔNG VÀO CHO ỨNG DỤNG SERVERLESS TRÊN AWS

Khi học AWS, mình thường bắt đầu từ Lambda — viết function xử lý logic rồi chạy thử. Nhưng làm sao để user bên ngoài gọi được Lambda đó qua HTTP? Ban đầu mình nghĩ phải dựng server Nginx hoặc Express.js làm reverse proxy. Sau đó mình mới biết Amazon API Gateway chính là "cổng vào" giúp expose API ra internet một cách an toàn, không cần quản lý server.

Amazon API Gateway là dịch vụ quản lý API fully managed — nhận HTTP/HTTPS request từ client, xác thực, giới hạn tốc độ (throttling), rồi chuyển tiếp tới backend (Lambda, HTTP endpoint, AWS service). Tích hợp Lambda, Step Functions, DynamoDB, SQS; built-in authentication, rate limiting, CORS, logging — hoàn toàn serverless.

#### REST API vs HTTP API — chọn loại nào?

| Tiêu chí | HTTP API | REST API |
| --- | --- | --- |
| Chi phí | Rẻ hơn (~70%) | Đắt hơn |
| Độ trễ | Thấp hơn | Cao hơn một chút |
| Tính năng | Cơ bản, đủ dùng | Đầy đủ (API key, request validation, WAF) |
| Phù hợp | Lambda proxy, app đơn giản | Enterprise, cần kiểm soát chặt |

Gợi ý: bắt đầu với **HTTP API**. Chỉ chuyển sang REST API khi cần tính năng nâng cao.

#### Use case: API đặt hàng serverless

```
Client (Web/Mobile)
    → API Gateway (POST /orders)
        → Lambda (Create Order)
            → DynamoDB (lưu order)
            → SQS (xử lý bất đồng bộ)
    ← 201 Created
```

Luồng đơn giản: Client gửi `POST /orders` kèm JSON body → API Gateway validate request, invoke Lambda → Lambda xử lý, trả response → API Gateway forward response về client.

#### Tính năng hữu ích

| Tính năng | Làm gì |
| --- | --- |
| **CORS** | Cho phép frontend gọi API từ domain khác |
| **Throttling** | Giới hạn request/giây, chống DDoS cơ bản |
| **API Key / Authorizer** | Xác thực request (JWT, Cognito, Lambda authorizer) |
| **Stage (dev/prod)** | Tách môi trường: `/dev/orders` vs `/prod/orders` |
| **CloudWatch Logs** | Ghi log mọi request để debug |

#### API Gateway trong bức tranh serverless

```
API Gateway  →  Lambda  →  DynamoDB
            →  Lambda  →  SQS  →  Lambda
            →  Step Functions  →  ...
```

API Gateway đứng ở đầu kiến trúc — lớp "presentation" nhận request từ bên ngoài; logic nghiệp vụ nằm ở Lambda/Step Functions phía sau.

Các điểm chính cần nắm:

* **HTTP API** đủ cho hầu hết project nhỏ–vừa — rẻ và nhanh.
* Luôn bật **CloudWatch Logs** khi debug — xem request/response chi tiết.
* Đừng expose Lambda trực tiếp — API Gateway có throttling, auth, HTTPS sẵn.

API Gateway là bước đầu tiên khi build API trên AWS. Không cần server, không cần cấu hình Nginx — chỉ cần map route tới Lambda là có API production-ready. Kết hợp với SQS, Step Functions phía sau, bạn có một kiến trúc serverless hoàn chỉnh.

**Tài liệu tham khảo:**

* [Amazon API Gateway – AWS Documentation](https://docs.aws.amazon.com/apigateway/)
* [Choose between HTTP APIs and REST APIs – AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)
* [Create an HTTP API – AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
