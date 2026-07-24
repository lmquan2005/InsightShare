---
title: "Week 4 Worklog"
date: 2026-07-06
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 objectives

* Learn Amazon S3: buckets, objects, storage classes and access control.
* Practice upload/download, versioning and lifecycle policies.
* Understand S3 as the storage foundation for Data Engineering pipelines.

### Tasks during the week (06/07 - 10/07/2026)

| Day | Task | Start | End | Reference |
| --- | --- | --- | --- | --- |
| Mon | Study S3: buckets, object keys, regions; compare storage classes (Standard, IA, Glacier). | 06/07/2026 | 06/07/2026 | [S3](https://docs.aws.amazon.com/s3/) |
| Tue | Learn bucket policies, ACLs, Block Public Access; configure secure access. | 07/07/2026 | 07/07/2026 | [S3 Security](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control.html) |
| Wed | Study versioning, lifecycle rules and prefix folder structure for a data lake. | 08/07/2026 | 08/07/2026 | [S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) |
| Thu | **Practice:** create a bucket, upload files via Console and CLI (`aws s3 cp`, `aws s3 ls`). | 09/07/2026 | 09/07/2026 | [AWS CLI S3](https://docs.aws.amazon.com/cli/latest/reference/s3/) |
| Fri | **Practice:** enable versioning, create lifecycle rules; organize bucket with `raw/`, `processed/`. | 10/07/2026 | 10/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |

### Results achieved

1. Understood how S3 stores objects and which storage classes suit different data types.
2. Configured bucket policies, versioning and basic lifecycle policies.
3. Performed upload/download via Console and CLI; organized folder structure for a data lake.
