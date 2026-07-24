---
title: "Blog 1"
date: 2026-07-24
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON SQS: HÀNG ĐỢI TIN NHẮN GIÚP HỆ THỐNG AWS KHÔNG BỊ "NGHẼN"

Amazon SQS (Simple Queue Service) là dịch vụ hàng đợi tin nhắn serverless trên AWS, giúp các thành phần trong hệ thống gửi và nhận message bất đồng bộ mà không cần kết nối trực tiếp. Thay vì Service A gọi thẳng Service B, flow sẽ là Service A → SQS → Service B — giảm coupling, hấp thụ traffic spike và không cần tự host RabbitMQ/Redis trên EC2.

#### Hai loại queue

| Loại | Đặc điểm | Phù hợp khi |
| --- | --- | --- |
| **Standard Queue** | Throughput cao, at-least-once delivery, có thể trùng/thứ tự lệch | Xử lý email, log, analytics |
| **FIFO Queue** | Đúng thứ tự, exactly-once processing, throughput thấp hơn | Thanh toán, đặt hàng, chat thread |

Ngoài ra còn có **Dead Letter Queue (DLQ)** — hàng đợi chứa message lỗi sau nhiều lần retry; **Visibility Timeout** — thời gian message "ẩn" khỏi queue khi đang được xử lý; **Long Polling** — giảm số lần gọi API rỗng, tiết kiệm chi phí.

#### Vì sao không nên gọi API/Lambda trực tiếp?

| Cách làm | Vấn đề |
| --- | --- |
| API gọi thẳng Lambda xử lý nặng | User phải chờ, timeout dễ xảy ra |
| Tự host RabbitMQ/Redis trên EC2 | Phải quản lý server, HA, backup |
| Retry thủ công trong code | Logic phức tạp, khó debug |
| Scale đồng thời khi traffic spike | Downstream service bị quá tải |

SQS giải quyết bằng cách tách producer và consumer: producer chỉ đẩy message vào queue → phản hồi nhanh; consumer (Lambda, EC2, ECS…) xử lý khi rảnh, scale theo số message; message không mất khi consumer tạm down; spike traffic được "hấp thụ" bởi queue thay vì làm sập backend.

Các điểm chính cần nắm:

* **Use case e-commerce:** API nhận đơn hàng → lưu DynamoDB → đẩy SQS → trả 201 ngay; Lambda consumer xử lý ngầm gửi email, cập nhật kho, sync CRM.
* **Integration phổ biến:** Lambda event source mapping, SNS fan-out → SQS, EventBridge route event, EC2/ECS worker polling, Step Functions.
* **Best practices:** luôn gắn DLQ; viết idempotent consumer (at-least-once); cấu hình VisibilityTimeout phù hợp; dùng long polling; monitor CloudWatch (`ApproximateNumberOfMessagesVisible`, `AgeOfOldestMessage`).

#### Chi phí

| Hạng mục | Giá |
| --- | --- |
| Free tier | 1 triệu request/tháng (permanent) |
| Standard queue | ~$0.40 / triệu request |
| FIFO queue | ~$0.50 / triệu request |
| Duy trì queue | Miễn phí |
| Data transfer trong cùng region | Miễn phí |

SQS là lớp đệm nền tảng cho kiến trúc event-driven trên AWS. Nếu mới học serverless, nên thử flow đơn giản: API Gateway → Lambda (producer) → SQS → Lambda (consumer) để thấy rõ sự khác biệt giữa xử lý đồng bộ và bất đồng bộ.

**Tài liệu tham khảo:**

* [Amazon SQS – AWS Documentation](https://docs.aws.amazon.com/sqs/)
* [SQS Best Practices – AWS Documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-best-practices.html)
* [How AutoScout24 built a Bot Factory with Amazon Bedrock](https://aws.amazon.com/blogs/)
