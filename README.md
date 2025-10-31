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

<img width="1919" height="951" alt="Image" src="https://github.com/user-attachments/assets/d6b6bd94-d4b1-4bce-a5fc-921f45ed31db" />

### 3. Data Processing
- **Azure Databricks** handles data cleansing, transformation, and enrichment.
- Implemented using **PySpark** and **SQL** notebooks.
- Transformations include:
  - Customer segmentation  
  - Demographic enrichment  
  - Churn probability scoring

🗄️ Database Setup
Below is the SQL script to create and populate the database tables (`products`, `stores`, and `transactions`):

```sql 
-- Products Table
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price INT
);

INSERT INTO products VALUES 
(1, 'Wireless Mouse', 'Electronics', 800),
(2, 'Bluetooth Speaker', 'Electronics', 1200),
(3, 'Yoga Mat', 'Fitness', 499),
(4, 'Laptop Stand', 'Accessories', 999),
(5, 'Notebook Set', 'Stationery', 149),
(6, 'Water Bottle', 'Fitness', 299),
(7, 'Smartwatch', 'Electronics', 4999),
(8, 'Desk Organizer', 'Accessories', 399),
(9, 'Dumbbell Set', 'Fitness', 1999),
(10, 'Pen Drive 32GB', 'Electronics', 599);

-- Stores Table
CREATE TABLE stores (
    store_id INT PRIMARY KEY,
    store_name VARCHAR(100),
    location VARCHAR(100)
);

INSERT INTO stores VALUES 
(1, 'City Mall Store', 'UAE'),
(2, 'High Street Store', 'Saudi Arabia'),
(3, 'Tech World Outlet', 'Qatar'),
(4, 'Cairo Festival City Mall', 'Egypt'),
(5, 'Mega Plaza', 'Kuwait');

-- Transactions Table
CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    store_id INT,
    quantity INT,
    transaction_date DATE,
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    FOREIGN KEY (store_id) REFERENCES stores(store_id)
);

INSERT INTO transactions VALUES 
(31, 101, 1, 1, 3, '2025-04-01'),
(32, 102, 2, 2, 2, '2025-04-03'),
(33, 103, 3, 3, 1, '2025-04-05'),
(34, 104, 4, 4, 5, '2025-04-07'),
(35, 105, 5, 5, 2, '2025-04-09'),
(36, 106, 6, 1, 4, '2025-04-11'),
(37, 107, 7, 2, 1, '2025-04-13'),
(38, 108, 8, 3, 3, '2025-04-15'),
(39, 109, 9, 4, 2, '2025-04-17'),
(40, 110, 10, 5, 5, '2025-04-19'),
(41, 111, 1, 1, 1, '2025-04-21'),
(42, 112, 2, 2, 4, '2025-04-23'),
(43, 113, 3, 3, 2, '2025-04-25'),
(44, 114, 4, 4, 3, '2025-04-27'),
(45, 115, 5, 5, 1, '2025-04-29'),
(46, 116, 6, 1, 2, '2025-05-01'),
(47, 117, 7, 2, 5, '2025-05-03'),
(48, 118, 8, 3, 3, '2025-05-05'),
(49, 119, 9, 4, 4, '2025-05-07'),
(50, 120, 10, 5, 2, '2025-05-09'),
(51, 121, 1, 1, 3, '2025-05-11'),
(52, 122, 2, 2, 4, '2025-05-13'),
(53, 123, 3, 3, 2, '2025-05-15'),
(54, 124, 4, 4, 5, '2025-05-17'),
(55, 125, 5, 5, 1, '2025-05-19'),
(56, 126, 6, 1, 4, '2025-05-21'),
(57, 127, 7, 2, 2, '2025-05-23'),
(58, 101, 8, 3, 3, '2025-05-25'),
(59, 102, 9, 4, 5, '2025-05-27'),
(60, 103, 10, 5, 1, '2025-05-29'),
(61, 104, 1, 1, 2, '2025-06-01'),
(62, 105, 2, 2, 3, '2025-06-03'),
(63, 106, 3, 3, 4, '2025-06-05'),
(64, 107, 4, 4, 5, '2025-06-07'),
(65, 108, 5, 5, 1, '2025-06-09'),
(66, 109, 6, 1, 2, '2025-06-11'),
(67, 110, 7, 2, 3, '2025-06-13'),
(68, 111, 8, 3, 4, '2025-06-15'),
(69, 112, 9, 4, 5, '2025-06-17'),
(70, 113, 10, 5, 1, '2025-06-19'),
(71, 114, 1, 1, 3, '2025-06-21'),
(72, 115, 2, 2, 2, '2025-06-23'),
(73, 116, 3, 3, 1, '2025-06-25'),
(74, 117, 4, 4, 4, '2025-06-27'),
(75, 118, 5, 5, 5, '2025-06-29'),
(76, 119, 6, 1, 2, '2025-07-01'),
(77, 120, 7, 2, 3, '2025-07-03'),
(78, 121, 8, 3, 4, '2025-07-05'),
(79, 122, 9, 4, 1, '2025-07-07'),
(80, 123, 10, 5, 2, '2025-07-09');
```

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

```python
[notebook]()
```
---

## 🎯 Outcome
This solution creates a **single source of truth** for customer analytics, enabling:
- Data-driven decision making  
- Improved marketing segmentation  
- Real-time performance tracking via automated KPIs  
