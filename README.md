# Azure Databricks Medallion Architecture ETL Pipeline

An end-to-end data pipeline built on Azure Databricks using PySpark, Delta Lake, and Azure Data Lake Storage (ADLS) Gen2, orchestrated with Databricks Workflows and integrated with Snowflake.

## 🏗️ Architecture & Flow

1. **Ingestion (Bronze/Raw):** Fetches JSON data from REST APIs using Python `requests` with retry logic, writing payloads into ADLS Gen2 as raw Delta Lake tables.
2. **Transformation (Silver):** Cleanses schema types, flattens nested JSON structures (`dimensions`, `meta`), applies PySpark Data Quality validation gates, and deduplicates key records.
3. **Data Warehouse (Gold):** Serves curated datasets to Snowflake for downstream BI and analytics queries.
4. **Security & Governance:** Authenticates to ADLS Gen2 via Azure Key Vault Secret Scopes using Service Principal OAuth 2.0 tokens.
5. **Orchestration:** Managed via multi-task Databricks Workflows with sequential dependencies (`Ingest` -> `Transform`).

## 🛠️ Tech Stack
* **Cloud Platform:** Azure (ADLS Gen2, Azure Key Vault, Service Principal)
* **Processing Framework:** PySpark, Spark SQL, Delta Lake
* **Orchestration:** Databricks Workflows
* **Target Warehouse:** Snowflake
* **Language:** Python, SQL

## 📁 Notebooks
* `01_setup_key_vault_oauth.py`: Session credential configuration for ADLS Gen2 OAuth.
* `02_ingest_products_api.py`: REST API ingestion with retry handling and Delta Lake output.
* `03_transform_raw_to_silver.py`: Silver layer cleansing, struct flattening, DQ gates, and deduplication.
