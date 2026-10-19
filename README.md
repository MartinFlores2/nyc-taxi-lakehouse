# 🚖 NYC Taxi Lakehouse & Data Pipeline

## 🎯 Business Impact & Value Proposition
In modern data-driven enterprises, raw data is a liability if not properly managed. This project addresses critical business challenges by transforming raw, messy transportation telemetry into **reliable, audit-ready analytical assets**. 

* **Data Reliability & Trust:** Implemented strict Data Quality checks and schema enforcement to prevent corrupted or anomalous data from reaching business stakeholders, ensuring 100% trust in executive dashboards.
* **Cost Efficiency & Performance:** Leveraged Delta Lake optimization, partitioning, and idempotent pipelines to eliminate redundant storage costs and reduce query execution times.
* **Operational Resilience:** Designed fully **idempotent pipelines** using `MERGE INTO` strategies, ensuring system recovery without data duplication, data drift, or pipeline failures during re-runs.
* **Decision-Ready Analytics:** Structured data under a Kimball dimensional model (Facts & Dimensions), enabling rapid business intelligence queries for dynamic pricing, route optimization, and resource allocation.

---

## 🏗️ Architecture & Medallion Design
The pipeline follows the robust **Medallion Architecture** pattern using PySpark, Delta Lake, and Databricks:

1. **Bronze Layer (Raw & Ingestion):** Ingests raw public parquet files from the NYC TLC data source without alterations, establishing a secure, immutable historical landing zone with automated DDL enforcement.
2. **Silver Layer (Cleaned & Filtered):** Applies exploratory data analysis (EDA), removes anomalies (negative fares, invalid coordinates, nulls), enforces data quality rules, and persists clean data using **idempotent MERGE operations**.
3. **Gold Layer (Business Aggregations & Modeling):** Implements a dimensional model (Kimball methodology: Facts and Dimensions) to deliver high-performance, business-ready metrics and aggregations.

---

## ⚙️ Key Technical Stack & Batch Highlights
* **Processing Framework:** PySpark, Spark SQL (Distributed processing for large-scale datasets).
* **Storage Format:** Delta Lake (ACID transactions, time travel, schema enforcement).
* **Pipeline Patterns:** 
  * Idempotent architecture (Zero duplication on re-runs).
  * Automated Data Quality gates.
  * Modular folder structure separating configuration, cleaning, modeling, and DDLs.
* **Workflow Management:** Orchestrated batch flows ensuring deterministic execution.

---

## 📁 Repository Structure
```text
nyc-taxi-lakehouse/
│
├── config/                  # Global configurations and environment paths
├── 01_bronze/               # Raw ingestion, DDLs, and initial bronze data quality
├── 02_silver/               # EDA, cleaning, transformations, and idempotent MERGE logic
├── 03_gold/                 # Kimball dimensional modeling (Facts/Dims) and aggregations
└── orchestrator/            # End-to-end pipeline execution runner
