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
# Databricks notebook source
spark.conf.set(
  "fs.azure.account.key.mariamstorageaccount123.dfs.core.windows.net",
  "tI6bWp5XyyKBhDYdcSuJIhHbkh6kXVYtNFkyOUt+hfJVEyUWq21njb21Irnkw6ojMuifGyLziShe+AStGlVL3g==")


df_products = spark.read.parquet("abfss://retail@mariamstorageaccount123.dfs.core.windows.net/dbo.products.parquet")
df_products.show(5)

df_transaction = spark.read.parquet("abfss://retail@mariamstorageaccount123.dfs.core.windows.net/dbo.transactions.parquet")
df_transaction.show(5)

df_stores= spark.read.parquet("abfss://retail@mariamstorageaccount123.dfs.core.windows.net/dbo.stores.parquet")
df_stores.show(5)

df_customers = spark.read.parquet("abfss://retail@mariamstorageaccount123.dfs.core.windows.net/MohammedHameds/Retails_Project/refs/heads/main/dataset/customers.parquet")
df_customers.show(5)

df_stores.write.mode("overwrite").saveAsTable("cat1.sales.store_bronze")

df_transaction.write.mode("overwrite").saveAsTable("cat1.sales.transactions_bronze")

df_products.write.mode("overwrite").saveAsTable("cat1.sales.products_bronze")

df_customers.write.mode("overwrite").saveAsTable("cat1.sales.customers_bronze")

display(df_customers)
df_customers.printSchema()

display(df_stores)
df_stores.printSchema()

display(df_transaction)
df_transaction.printSchema()

display(df_products)
df_products.printSchema()

from pyspark.sql.functions import col
df_customers = df_customers.select(
    col("customer_id").cast("int"),
    col("full_name"),
    col("email"),
    col("country"),
    col( "registration_date").cast("date")
)
df_customers.printSchema()

df_ratials_silver = df_transaction.join(df_customers,"customer_id").join(df_products,"product_id").join(df_stores,"store_id")
df_ratials_silver.write.mode("overwrite").saveAsTable("cat1.sales.retails_silver")

from pyspark.sql.functions import sum, count
df_sales_by_country = df_ratials_silver.groupBy("country").agg(count("transaction_id").alias("total_sales"))
df_sales_by_country.write.mode("overwrite").saveAsTable("cat1.sales.sales_by_country_gold")

customer_product_affinity = df_ratials_silver.groupBy("customer_id", "full_name", "product_id", "product_name", "category") \
    .agg(
        sum("quantity").alias("total_quantity_purchased"),
        count("transaction_id").alias("purchase_frequency")
    ) \
    .orderBy("customer_id", col("total_quantity_purchased").desc())

customer_product_affinity.write.mode("overwrite").saveAsTable("cat1.sales.customer_product_affinity_gold")

store_product_performance = df_ratials_silver.groupBy("store_id", "store_name", "product_id", "product_name") \
    .agg(
        sum("quantity").alias("quantity_sold"),
        sum(col("quantity") * col("price")).alias("revenue_generated")
    ) \
    .orderBy("store_id", col("revenue_generated").desc())

store_product_performance.write.mode("overwrite").saveAsTable("cat1.sales.store_product_performance_gold")

from pyspark.sql import functions as F
from pyspark.sql.functions import col, sum, avg, count, countDistinct, month, year, quarter, datediff, current_date, max as max_, min as min_



price_segment_analysis = df_ratials_silver \
    .withColumn("price_segment", 
                F.when(col("price") < 500, "Budget")
                 .when(col("price") < 1500, "Mid-Range")
                 .otherwise("Premium")) \
    .groupBy("price_segment", "category") \
    .agg(
        count("transaction_id").alias("transaction_count"),
        sum("quantity").alias("total_quantity"),
        sum(col("quantity") * col("price")).alias("total_revenue")
    ) \
    .orderBy("price_segment", col("total_revenue").desc())

price_segment_analysis.write.mode("overwrite").saveAsTable("cat1.sales.price_segment_analysis_gold")

seasonal_analysis = df_ratials_silver \
    .withColumn("month", month("transaction_date")) \
    .withColumn("season",
                F.when(col("month").isin(12, 1, 2), "Winter")
                 .when(col("month").isin(3, 4, 5), "Spring")
                 .when(col("month").isin(6, 7, 8), "Summer")
                 .otherwise("Fall")) \
    .groupBy("season", "category") \
    .agg(
        sum(col("quantity") * col("price")).alias("seasonal_revenue"),
        sum("quantity").alias("seasonal_quantity")
    ) \
    .orderBy("season", col("seasonal_revenue").desc())

seasonal_analysis.write.mode("overwrite").saveAsTable("cat1.sales.seasonal_analysis_gold")

category_country_performance = df_ratials_silver.groupBy("country", "category") \
    .agg(
        sum(col("quantity") * col("price")).alias("revenue"),
        sum("quantity").alias("quantity_sold"),
        countDistinct("product_id").alias("unique_products")
    ) \
    .orderBy("country", col("revenue").desc())

category_country_performance.write.mode("overwrite").saveAsTable("cat1.sales.category_country_performance_gold")


country_detailed_analysis = df_ratials_silver.groupBy("country") \
    .agg(
        countDistinct("customer_id").alias("unique_customers"),
        countDistinct("store_id").alias("unique_stores"),
        count("transaction_id").alias("total_transactions"),
        sum("quantity").alias("total_quantity_sold"),
        sum(col("quantity") * col("price")).alias("total_revenue"),
        avg(col("quantity") * col("price")).alias("avg_transaction_value"),
        countDistinct("product_id").alias("unique_products")
    ) \
    .orderBy(col("total_revenue").desc())


country_detailed_analysis.write.mode("overwrite").saveAsTable("cat1.sales.country_detailed_analysis_gold")

country_detailed_analysis.write.mode("overwrite").saveAsTable("cat1.sales.country_detailed_analysis_gold")


store_customer_analysis = df_ratials_silver.groupBy("store_id", "store_name", "location") \
    .agg(
        countDistinct("customer_id").alias("unique_customers"),
        count("transaction_id").alias("total_transactions")
    ) \
    .withColumn("avg_transactions_per_customer", col("total_transactions") / col("unique_customers")) \
    .orderBy(col("unique_customers").desc())


store_customer_analysis.write.mode("overwrite").saveAsTable("cat1.sales.store_customer_analysis_gold")


from pyspark.sql.functions import month, year, quarter


monthly_sales = df_ratials_silver \
    .withColumn("transaction_month", month("transaction_date")) \
    .withColumn("transaction_year", year("transaction_date")) \
    .withColumn("transaction_quarter", quarter("transaction_date")) \
    .groupBy("transaction_year", "transaction_quarter", "transaction_month") \
    .agg(
        sum(col("quantity") * col("price")).alias("monthly_revenue"),
        sum("quantity").alias("monthly_quantity"),
        countDistinct("transaction_id").alias("monthly_transactions"),
        countDistinct("customer_id").alias("monthly_customers")
    ) \
    .orderBy("transaction_year", "transaction_month")


monthly_sales.write.mode("overwrite").saveAsTable("cat1.sales.monthly_sales_gold")


product_performance = df_ratials_silver.groupBy("product_id", "product_name", "category") \
    .agg(
        sum("quantity").alias("total_quantity_sold"),
        sum(col("quantity") * col("price")).alias("total_revenue"),
        countDistinct("transaction_id").alias("unique_transactions"),
        countDistinct("customer_id").alias("unique_customers")
    ) \
    .orderBy(col("total_revenue").desc())

product_performance.write.mode("overwrite").saveAsTable("cat1.sales.product_performance_gold")


customer_registration_trends = df_customers \
    .withColumn("reg_month", month("registration_date")) \
    .withColumn("reg_year", year("registration_date")) \
    .groupBy("reg_year", "reg_month", "country") \
    .agg(count("customer_id").alias("new_customers")) \
    .orderBy("reg_year", "reg_month")
```

---

## 🎯 Outcome
This solution creates a **single source of truth** for customer analytics, enabling:
- Data-driven decision making  
- Improved marketing segmentation  
- Real-time performance tracking via automated KPIs  
