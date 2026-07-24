---
title: "Blog 2"
date: 2026-07-24
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS STEP FUNCTIONS: ĐIỀU PHỐI WORKFLOW NHIỀU BƯỚC MÀ KHÔNG VIẾT CODE PHỨC TẠP

Khi học AWS, mình thường dùng Lambda xử lý từng tác vụ riêng lẻ. Nhưng khi workflow có nhiều bước — validate → xử lý → gửi email → cập nhật DB — code Lambda dễ thành "spaghetti". AWS Step Functions giúp gom các bước đó thành một luồng rõ ràng, có retry và xử lý lỗi sẵn.

Step Functions là dịch vụ điều phối workflow serverless. Bạn định nghĩa các bước (states) bằng JSON (Amazon States Language), Step Functions tự chạy tuần tự hoặc song song, retry khi lỗi.

#### Các loại state phổ biến

| State | Mô tả |
| --- | --- |
| **Task** | Gọi Lambda, ECS, SNS, DynamoDB, Bedrock… |
| **Choice** | Rẽ nhánh theo điều kiện (if/else) |
| **Parallel** | Chạy nhiều nhánh cùng lúc |
| **Wait** | Chờ một khoảng thời gian |
| **Fail / Succeed** | Kết thúc workflow |

#### Hai loại workflow

| Loại | Đặc điểm | Phù hợp khi |
| --- | --- | --- |
| **Standard** | Chạy tối đa 1 năm, exactly-once | Order processing, ETL, approval flow |
| **Express** | Chạy tối đa 5 phút, throughput cao | IoT, streaming, real-time |

#### Use case: Xử lý đơn hàng

```
API nhận đơn hàng
    → Step Functions bắt đầu
        → Lambda: Validate order
        → Choice: hợp lệ?
            → Có: Lambda xử lý + SES gửi email (song song)
            → Không: Fail + SNS thông báo lỗi
```

#### So với Lambda thuần

| Tiêu chí | Lambda thuần | Step Functions |
| --- | --- | --- |
| Workflow nhiều bước | Code phức tạp, khó đọc | Visual, dễ theo dõi |
| Retry / error handling | Tự viết | Built-in |
| Chạy song song | Tự implement | Parallel state |
| Giám sát | CloudWatch Logs | Execution history từng bước |

Các điểm chính cần nắm:

* Dùng Step Functions khi có **3+ bước** hoặc cần retry/branch rõ ràng.
* **Standard** cho workflow dài; **Express** cho real-time ngắn.
* Xem **execution graph** trên console — debug dễ hơn đọc log Lambda.

Step Functions không thay thế Lambda — nó điều phối Lambda. Khi workflow phức tạp hơn một function, hãy thử Step Functions: ít code hơn, dễ bảo trì hơn, và có sẵn retry/error handling.

**Tài liệu tham khảo:**

* [AWS Step Functions – AWS Documentation](https://docs.aws.amazon.com/step-functions/)
* [Amazon States Language – AWS Documentation](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)
