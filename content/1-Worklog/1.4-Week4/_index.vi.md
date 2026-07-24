---
title: "Worklog Tuần 4"
date: 2026-07-06
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4

* Nắm Amazon S3: bucket, object, storage class và cơ chế phân quyền.
* Thực hành upload/download, versioning và lifecycle policy.
* Hiểu S3 là nền tảng lưu trữ dữ liệu cho pipeline Data Engineering.

### Các công việc triển khai trong tuần (06/07 - 10/07/2026)

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| T2 | Tìm hiểu S3: bucket, object key, region; so sánh storage class (Standard, IA, Glacier). | 06/07/2026 | 06/07/2026 | [S3](https://docs.aws.amazon.com/s3/) |
| T3 | Học bucket policy, ACL, Block Public Access; cấu hình quyền truy cập an toàn. | 07/07/2026 | 07/07/2026 | [S3 Security](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control.html) |
| T4 | Tìm hiểu versioning, lifecycle rule và cấu trúc thư mục prefix cho data lake. | 08/07/2026 | 08/07/2026 | [S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) |
| T5 | **Thực hành:** tạo bucket, upload file qua Console và CLI (`aws s3 cp`, `aws s3 ls`). | 09/07/2026 | 09/07/2026 | [AWS CLI S3](https://docs.aws.amazon.com/cli/latest/reference/s3/) |
| T6 | **Thực hành:** bật versioning, tạo lifecycle rule; tổ chức bucket theo `raw/`, `processed/`. | 10/07/2026 | 10/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được

1. Hiểu cách S3 lưu trữ object và các storage class phù hợp từng loại dữ liệu.
2. Cấu hình bucket policy, versioning và lifecycle policy cơ bản.
3. Thao tác upload/download qua Console và CLI; tổ chức cấu trúc thư mục cho data lake.
