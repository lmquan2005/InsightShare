---
title: "Week 6 Worklog"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 objectives

* Learn AWS Glue Data Catalog, Crawlers and ETL Jobs.
* Practice auto-discovering schemas and transforming data from `raw/` to `processed/`.
* Clean data: remove nulls, change column types, export Parquet.

### Tasks during the week (20/07 - 24/07/2026)

| Day | Task | Start | End | Reference |
| --- | --- | --- | --- | --- |
| Mon | Study Glue Data Catalog: databases, tables, partitions; role of crawlers. | 20/07/2026 | 20/07/2026 | [Glue Catalog](https://docs.aws.amazon.com/glue/latest/dg/catalog-and-crawler.html) |
| Tue | **Practice:** create IAM role, database and crawler pointing to S3 `raw/`; run crawler. | 21/07/2026 | 21/07/2026 | [Glue Crawler](https://docs.aws.amazon.com/glue/latest/dg/add-crawler.html) |
| Wed | Study Glue ETL Jobs: Spark, DPUs; transforms — drop nulls, rename columns, filter. | 22/07/2026 | 22/07/2026 | [Glue ETL](https://docs.aws.amazon.com/glue/latest/dg/etl-jobs-section.html) |
| Thu | **Practice:** create ETL job reading raw table, clean data and write Parquet to `processed/`. | 23/07/2026 | 23/07/2026 | [Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| Fri | Run job, verify S3 output; re-run crawler to update Catalog metadata. | 24/07/2026 | 24/07/2026 | [Glue Studio](https://docs.aws.amazon.com/glue/latest/ug/what-is-glue-studio.html) |

### Results achieved

1. Understood Glue Data Catalog and how crawlers auto-discover schemas.
2. Created an ETL job transforming raw to processed data with basic cleaning steps.
3. Exported Parquet data to S3 and updated Catalog metadata.
