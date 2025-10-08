# 🚀 ETE Databricks Medallion Project

## 🔹 Overview
End-to-end data engineering project implemented on **Databricks** using **ADLS Gen2, Unity Catalog, Autoloader, and Delta Live Tables**.  
The goal was to build a **medallion architecture (Bronze → Silver → Gold)** enforcing **star schema** at the gold layer.

---

## 🔹 Data Sources
Input files placed by source team into **ADLS Gen2 `source` container**:

- `region/` → Lookup dataset (one-time load)  
- `customers/` → Dimension table (**SCD Type 1**)  
- `products/` → Dimension table (**SCD Type 2 with DLT**)  
- `orders/` → Fact table  

---

## 🔹 Architecture

### Bronze Layer
- **Region dataset** → Ingested via **Databricks data ingestion UI** (no code).  
- **Customers, Products, Orders** → Ingested via **Autoloader** (structured streaming with checkpointing).  
- All tables registered under **Unity Catalog**.  

### Silver Layer
- Transformations applied to **clean, standardize, and join** datasets.  
- Stored as **Delta tables** in the Silver schema.  

### Gold Layer
- **Customers** → Implemented **SCD Type 1** (overwrite updates).  
- **Products** → Implemented **SCD Type 2** (historical tracking using Delta Live Tables).  
- **Orders** → Fact table, joined with dimensions.  
- Final schema enforces **star schema** for analytics.  

---

## 🔹 Tech Stack
- Databricks
- Metastore Creation and Workspace assignment.
- Access Connector for Azure Databricks.
- AutoLoader capabilities of Spark Structured Streaming.
- Basic and Advanced PySpark functions.
- Azure Data Lake Storage Gen2 (ADLS Gen2)  
- Delta Lake (Bronze / Silver / Gold layers)
- SCD - Type 1 and SCD - Type 2 using DLT

---

## 🔹 Project Flow Diagram
Example:
```bash
/docs/architecture.png
