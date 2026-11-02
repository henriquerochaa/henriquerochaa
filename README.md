# Henrique Daniel da Rocha

**Software Engineer + Data Engineering | Python · SQL · AWS**

[LinkedIn](https://www.linkedin.com/in/henrique-daniel-rocha/) · henriquedan1702@gmail.com

I build batch and incremental data pipelines that are contract-checked, tested and safe to re-run: ingestion with Python, transformations with dbt and DuckDB, orchestration with Airflow, publication to Postgres. I apply software engineering practices to data: input contracts, tests at every layer, static typing and CI. I have also taught programming in a vocational Systems Development program, and I am looking for my first data engineering role.

**Education:** Software Engineering.

**Start here:** [olist-delivery-review-pipeline](https://github.com/henriquerochaa/olist-delivery-review-pipeline) is the complete project, with tests and documented limits.

## Focus

- **Software engineering:** backend (Python, Django, DRF), automated testing, static typing, CI
- **Data engineering:** ETL/ELT, batch pipelines, incremental API ingestion, orchestration
- **Modeling and architecture:** dimensional modeling, grain, medallion layers, warehouse, lake and lakehouse
- **Stack:** Python, SQL, Airflow, dbt, DuckDB, Parquet, Postgres, GitHub Actions
- **Cloud:** AWS (S3, IAM, VPC, RDS, Glue, Athena, Lambda), through study and labs

## Projects

### [olist-delivery-review-pipeline](https://github.com/henriquerochaa/olist-delivery-review-pipeline)

- **Problem:** how does delivery performance relate to review scores? Public Olist dataset, 8 sources, 550,759 rows.
- **Result:** late orders average 2.27 stars versus 4.29 for early ones (99,441 orders). Descriptive, not causal.
- **Flow:** CSV → Bronze (Parquet) → Silver and Gold (dbt) → Postgres (Neon), orchestrated by Airflow.
- **Key decision:** publishing checks the last `dbt build` and refuses a failed Gold, or one older than what is already published, then loads in a single transaction with a least-privilege role.
- **Known limits:** CSVs are read fully into memory, and concurrent runs of the same batch are not coordinated.
- **Evidence:** [data contracts](https://github.com/henriquerochaa/olist-delivery-review-pipeline/tree/main/contracts) · [43 Python tests](https://github.com/henriquerochaa/olist-delivery-review-pipeline/tree/main/tests) · [dbt models and tests](https://github.com/henriquerochaa/olist-delivery-review-pipeline/tree/main/dbt_pipeline_qualidade) · [Airflow DAG](https://github.com/henriquerochaa/olist-delivery-review-pipeline/tree/main/airflow)

`Python` `dbt` `DuckDB` `Airflow` `Postgres`

### [bcb-indicators-pipeline](https://github.com/henriquerochaa/bcb-indicators-pipeline)

- **Status:** v1.0 in progress.
- **Problem:** keep three Central Bank of Brazil series (USD PTAX, Selic target, monthly IPCA) up to date, incrementally and auditably.
- **Flow:** SGS API → Bronze (append per batch) → Silver (latest batch per key, rejected records kept apart) → Gold (monthly).
- **Key decision:** re-read window plus upsert on `(series, date)`, which captures retroactive revisions at the cost of re-reading recent data. Quality gate: `Bronze = Silver + rejected`.
- **Also:** offline CI with recorded API responses and a contract test for upstream format changes.

`Python` `DuckDB` `Parquet` `GitHub Actions`

## Principles

Re-runs must be safe · a contract or test failure stops the flow · grain is defined before the join · nothing is dropped silently · limits are documented, and what was not measured is not claimed.

## Knowledge Base

320+ personal study notes on data engineering: lifecycle, architecture, ingestion, orchestration, storage, modeling, data quality, engineering patterns and AWS. Books read in full: *Fundamentals of Data Engineering* and *Decifrando Arquiteturas de Dados*. Four more read selectively, guided by the projects. Coursera Data Engineering courses 1 to 4 and AWS Essential.

<details>
<summary>Topics by area, and where each became practice</summary>

| Area | Topics | In projects |
|---|---|:---:|
| **Lifecycle and fundamentals** | 5 stages and 6 undercurrents, requirements, security, build vs buy, cost | study |
| **Architecture** | Warehouse, lake, lakehouse, mesh, fabric, Lambda/Kappa, medallion, open table formats | practice (medallion) |
| **Sources and ingestion** | Relational and NoSQL, APIs, batch vs streaming, ETL/ELT, CDC, Kafka/Kinesis | practice (batch, API) |
| **Orchestration and DataOps** | Airflow, Terraform, observability, Great Expectations, data contracts | practice (Airflow, contracts) |
| **Storage and querying** | Columnar vs row, object/block/file, indexes, joins, Redshift, graph and vector DBs, streaming windows | practice (Parquet, DuckDB) |
| **Modeling and transformation** | Normalization, star schema, grain, Kimball/Inmon/Data Vault, SCD, dbt | practice (star schema, dbt) |
| **Data quality** | Quality dimensions, testing, anomalies, lineage, reconciliation | practice |
| **Engineering patterns** | Idempotency, error handling, ingestion, storage, observability | practice (idempotency) |
| **Analytical Python and SQL** | Pandas, time series, cohorts, anomaly detection, CTEs | practice |
| **AWS** | S3, EC2, IAM, VPC, RDS, DynamoDB, Lambda, Glue, Athena, CloudWatch | study and labs |

</details>

**Next:** Spark and Databricks, Delta Lake, orchestration beyond Airflow, AWS applied to analytical workloads.
