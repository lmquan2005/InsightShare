---
title: "Worklog Tuần 5"
date: 2026-07-13
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5

* Tìm hiểu Amazon RDS và thực hành kết nối database từ EC2.
* Làm quen khái niệm Data Engineering: ETL/ELT, data lake, định dạng dữ liệu.
* Chuẩn bị dữ liệu mẫu trên S3 cho các tuần thực hành tiếp theo.

### Các công việc triển khai trong tuần (13/07 - 17/07/2026)

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| T2 | Tìm hiểu RDS: engine, instance class, Multi-AZ, automated backup và snapshot. | 13/07/2026 | 13/07/2026 | [RDS](https://docs.aws.amazon.com/rds/) |
| T3 | **Thực hành:** tạo RDS MySQL trong subnet private; kết nối từ EC2 qua MySQL client. | 14/07/2026 | 14/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| T4 | Tìm hiểu Data Engineering: ETL/ELT, batch processing, data lake vs data warehouse. | 15/07/2026 | 15/07/2026 | [AWS Analytics](https://aws.amazon.com/big-data/datalakes-and-analytics/) |
| T5 | Học định dạng dữ liệu CSV, JSON, Parquet; lợi ích columnar format khi truy vấn. | 16/07/2026 | 16/07/2026 | [Athena](https://docs.aws.amazon.com/athena/latest/ug/columnar-storage.html) |
| T6 | **Thực hành:** tạo dữ liệu mẫu, upload lên S3 `raw/`; vẽ sơ đồ pipeline S3 → Glue → Athena. | 17/07/2026 | 17/07/2026 | [Glue](https://docs.aws.amazon.com/glue/) |

### Kết quả đạt được

1. Hiểu RDS managed database và thực hành kết nối, truy vấn SQL cơ bản.
2. Nắm khái niệm Data Engineering và vai trò của data lake trên S3.
3. Chuẩn bị dữ liệu mẫu và phác thảo kiến trúc pipeline cho đề tài.
