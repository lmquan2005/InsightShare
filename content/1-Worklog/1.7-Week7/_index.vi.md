---
title: "Worklog Tuần 7"
date: 2026-07-27
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7

* Tìm hiểu Amazon Athena: truy vấn SQL trực tiếp trên S3 qua Glue Catalog.
* Ghép pipeline end-to-end: S3 → Glue Crawler → Glue ETL → Athena.
* Theo dõi Glue job qua CloudWatch metric và log cơ bản.

### Các công việc triển khai trong tuần (27/07 - 31/07/2026)

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| T2 | Tìm hiểu Athena: serverless query engine, tích hợp Glue Catalog, chi phí data scanned. | 27/07/2026 | 27/07/2026 | [Athena](https://docs.aws.amazon.com/athena/) |
| T3 | **Thực hành:** truy vấn bảng `processed_sales`; SELECT, GROUP BY, JOIN cơ bản. | 28/07/2026 | 28/07/2026 | [Athena SQL](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html) |
| T4 | **Thực hành:** upload batch dữ liệu mới → chạy crawler → chạy ETL job → truy vấn Athena. | 29/07/2026 | 29/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| T5 | Tìm hiểu CloudWatch: metric Glue job (success/fail), log group, alarm cơ bản. | 30/07/2026 | 30/07/2026 | [CloudWatch](https://docs.aws.amazon.com/cloudwatch/) |
| T6 | Ghi lại lỗi gặp phải (permission, schema mismatch) và cách xử lý trong pipeline. | 31/07/2026 | 31/07/2026 |  |

### Kết quả đạt được

1. Truy vấn được dữ liệu trên S3 bằng Athena thông qua Glue Data Catalog.
2. Vận hành pipeline data end-to-end từ ingestion đến truy vấn.
3. Biết theo dõi Glue job qua CloudWatch và xử lý lỗi tích hợp thường gặp.
