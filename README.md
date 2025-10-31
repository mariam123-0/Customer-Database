# Customer Data Platform using Azure Databricks

## 📘 Overview
This project implements a **Customer Data Platform (CDP)** on **Microsoft Azure**, integrating multiple Azure services such as **Data Factory**, **Databricks**, and **Data Lake Storage**.  
The goal is to create a unified, analytics-ready **customer database** enriched with **KPIs** and data sourced from **external APIs**.

<img width="1047" height="424" alt="Image" src="https://github.com/user-attachments/assets/0128a11f-2eed-4fd7-a6f4-81db80fde4bd" />

---

## ⚙️ Architecture

### 1. Data Sources
Customer and behavioral data are collected from multiple sources:
- External APIs
- CRM systems
- Transactional databases
✨ [View API Config JSON](https://raw.githubusercontent.com/MohammedHameds/Retails_Project/refs/heads/main/dataset/customers.json)

### 2. Data Ingestion (ETL)
- **Azure Data Factory (ADF)** orchestrates ETL pipelines.
- Data is extracted from APIs and databases, transformed, and loaded into **Azure Data Lake Storage Gen2** for staging.

### 3. Data Processing
- **Azure Databricks** handles data cleansing, transformation, and enrichment.
- Implemented using **PySpark** and **SQL** notebooks.
- Transformations include:
  - Customer segmentation  
  - Demographic enrichment  
  - Churn probability scoring  

### 4. Data Modeling
- Processed data is stored in **Delta Tables** within Databricks.
- Ensures high performance, reliability, and version control.

### 5. KPI Development
Key business KPIs are automatically calculated and refreshed using Databricks jobs:
- Customer Lifetime Value (**CLV**)  
- Customer Retention Rate  
- Average Revenue per User (**ARPU**)  
- Customer Acquisition Cost (**CAC**)  
- Engagement and Churn Metrics  

### 6. Analytics & Reporting
The curated data is integrated with **Power BI** or **Azure Synapse Analytics** for:
- Real-time dashboards  
- KPI visualization  
- Business insights  

---

## 🧰 Technologies Used
- **Azure Data Factory** – ETL orchestration and API ingestion  
- **Azure Databricks** – Data transformation using **Python (PySpark)** and **SQL**  
- **Azure Data Lake Storage (Gen2)** – Centralized data storage  
- **Power BI / Synapse Analytics** – Data visualization and analytics  

---

## 🎯 Outcome
This solution creates a **single source of truth** for customer analytics, enabling:
- Data-driven decision making  
- Improved marketing segmentation  
- Real-time performance tracking via automated KPIs  
