---
title: "Worklog Tuần 6"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6

* Tìm hiểu AWS Glue Data Catalog, Crawler và ETL Job.
* Thực hành tự động phát hiện schema và transform dữ liệu từ `raw/` sang `processed/`.
* Làm sạch dữ liệu: loại null, đổi kiểu cột, xuất Parquet.

### Các công việc triển khai trong tuần (20/07 - 24/07/2026)

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| T2 | Tìm hiểu Glue Data Catalog: database, table, partition; vai trò của Crawler. | 20/07/2026 | 20/07/2026 | [Glue Catalog](https://docs.aws.amazon.com/glue/latest/dg/catalog-and-crawler.html) |
| T3 | **Thực hành:** tạo IAM role, database và crawler trỏ tới S3 `raw/`; chạy crawler. | 21/07/2026 | 21/07/2026 | [Glue Crawler](https://docs.aws.amazon.com/glue/latest/dg/add-crawler.html) |
| T4 | Tìm hiểu Glue ETL Job: Spark, DPU; transform drop null, rename column, filter. | 22/07/2026 | 22/07/2026 | [Glue ETL](https://docs.aws.amazon.com/glue/latest/dg/etl-jobs-section.html) |
| T5 | **Thực hành:** tạo ETL job đọc bảng raw, làm sạch và ghi vào `processed/` dạng Parquet. | 23/07/2026 | 23/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| T6 | Chạy job, kiểm tra output trên S3; chạy crawler lại để cập nhật Catalog. | 24/07/2026 | 24/07/2026 | [Glue Studio](https://docs.aws.amazon.com/glue/latest/ug/what-is-glue-studio.html) |

### Kết quả đạt được

1. Hiểu Glue Data Catalog và cách crawler tự động phát hiện schema.
2. Tạo ETL job transform dữ liệu từ raw sang processed với các bước làm sạch cơ bản.
3. Xuất dữ liệu Parquet lên S3 và cập nhật metadata trong Catalog.
