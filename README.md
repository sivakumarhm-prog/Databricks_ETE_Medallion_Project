# Databricks E2E Pipeline | Retail Dataset | Medallion Architecture

## Overview
This project implements an **End-to-End (E2E) Data Pipeline** using **Azure Databricks**, designed around the **Medallion Architecture** (Bronze, Silver, Gold layers) for efficient data ingestion, transformation, and governance. The pipeline processes a **Retail Dataset** and enforces a **Star Schema** at the Gold layer with **Slowly Changing Dimensions (SCD Type 1 & Type 2)** applied on dimension tables.

---

## Architecture Summary
- **Medallion Architecture Layers:**
  - **Bronze:** Raw ingestion layer using Databricks Autoloader.
  - **Silver:** Cleansed and curated data stored as Delta files.
  - **Gold:** Business-level data models (Star Schema) for analytics.

---

## Implementation Steps

1. **Source Setup**
   - Created a **source container** in **Azure Data Lake Storage Gen2 (ADLS Gen2)**.
   - Source team uploads input datasets into this container for ingestion.

2. **Data Governance & Access Configuration**
   - Created a new **Unity Catalog Metastore** and assigned it to the Databricks Workspace.
   - Set up **Access Connector for Azure Databricks** to securely connect Databricks with ADLS Gen2 storage accounts and containers.
   - Ensured compliance with high-grade data governance and RBAC control.

3. **Bronze Layer – Ingestion**
   - Implemented Databricks **Autoloader**, built on top of Spark’s **Structured Streaming**, for streaming ingestion.
   - Achieved **exactly-once** ingestion functionality into the **Bronze container**.

4. **Silver Layer – Transformation**
   - Performed required data cleaning and transformation on Bronze datasets.
   - Stored transformed data in the **Silver layer** as **Delta files**.
   - Created corresponding **Delta tables** for structured query capabilities.

5. **Gold Layer – Star Schema Modeling**
   - Enforced **Star Schema** design for analytical efficiency:
     - **Fact Table:** Orders Dataset  
     - **Dimension Tables:** Products, Customers
   - Stored datasets in the **Gold layer** using Delta format for performance optimization.

6. **Slowly Changing Dimensions (SCD) Enforcement**
   - **Customer Dimension:** Applied **SCD Type 1 (Upsert)** for direct updates.
   - **Products Dimension:** Applied **SCD Type 2 (Upsert with Data Lineage)** using **Delta Live Tables (DLT)** – Databricks' declarative ETL framework.

---

## Outcome
Successfully implemented an **End-to-End Pipeline** in Databricks with:
- Complete **Medallion Architecture** setup.
- Unified **Star Schema** model at the Gold layer.
- Data governance via **Unity Catalog**.
- Automated data lineage and versioning through **SCD type enforcement**.

The pipeline delivers scalable, governed, and high-performance data transformations ready for downstream analytics and BI reporting.

---

## Tech Stack
- **Platform:** Azure Databricks  
- **Storage:** ADLS Gen2  
- **Frameworks:** Autoloader, DLT (Delta Live Tables)  
- **Format:** Delta Lake  
- **Architecture:** Medallion (Bronze–Silver–Gold)  
- **Schema Model:** Star Schema  
- **Governance:** Unity Catalog

---

## Author
**Data Engineer:** Sivakumar Murugesan
**Date:** October 2025  
