---
title: "Week 7 Worklog"
date: 2026-07-27
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 objectives

* Learn Amazon Athena: run SQL queries directly on S3 via Glue Catalog.
* Build an end-to-end pipeline: S3 → Glue Crawler → Glue ETL → Athena.
* Monitor Glue jobs via basic CloudWatch metrics and logs.

### Tasks during the week (27/07 - 31/07/2026)

| Day | Task | Start | End | Reference |
| --- | --- | --- | --- | --- |
| Mon | Study Athena: serverless query engine, Glue Catalog integration, data scanned pricing. | 27/07/2026 | 27/07/2026 | [Athena](https://docs.aws.amazon.com/athena/) |
| Tue | **Practice:** query `processed_sales` table; basic SELECT, GROUP BY, JOIN. | 28/07/2026 | 28/07/2026 | [Athena SQL](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html) |
| Wed | **Practice:** upload new data batch → run crawler → run ETL job → query with Athena. | 29/07/2026 | 29/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| Thu | Study CloudWatch: Glue job metrics (success/fail), log groups, basic alarms. | 30/07/2026 | 30/07/2026 | [CloudWatch](https://docs.aws.amazon.com/cloudwatch/) |
| Fri | Document errors encountered (permissions, schema mismatch) and how they were resolved. | 31/07/2026 | 31/07/2026 |  |

### Results achieved

1. Queried S3 data with Athena through Glue Data Catalog.
2. Ran an end-to-end data pipeline from ingestion to query.
3. Monitored Glue jobs via CloudWatch and resolved common integration issues.
