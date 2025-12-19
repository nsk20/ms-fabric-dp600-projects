# 🛠️ Ingesting Data with Microsoft Fabric Pipelines (DP-600)

## Overview
This project demonstrates the implementation of a scalable **Extract, Transform, and Load (ETL)** solution using **Microsoft Fabric Pipelines**. [cite_start]The workflow automates the process of extracting raw data from an external source, managing intermediate storage, and executing custom **Apache Spark** logic to load processed data into Delta tables. 

## 🎯 Project Objectives
- [cite_start]Orchestrate a multi-stage data workflow using **Data Factory pipelines**. [cite: 1, 5]
- [cite_start]Ingest raw sales data from an external **HTTP source** via the Copy Data activity. [cite: 2, 3]
- [cite_start]Implement a **Parameterized Spark Notebook** for reusable data transformation logic. 
- [cite_start]Automate storage management using the **Delete Data activity** to ensure a clean landing zone for each run. 

## 🛠️ Pipeline Architecture
[cite_start]The final ETL process consists of three sequential activities: 

1.  [cite_start]**Delete Old Files:** Clears the `new_data` landing zone of existing CSV files using a wildcard (`*.csv`) to prevent data duplication. 
2.  **Copy Data (HTTP to OneLake):** Extracts a `sales.csv` file from a GitHub repository and loads it into the Lakehouse's `Files` storage. [cite: 2, 3]
3.  **Load Sales Notebook:** Triggers a Spark notebook that transforms the raw CSV data into a refined Delta table. 



## 💻 Transformation Logic (Spark)
The notebook processes raw data with the following transformations: [cite: 4]
- **Time Intelligence:** Extracts `Year` and `Month` from the order dates. [cite: 4]
- **String Manipulation:** Splits full customer names into separate `FirstName` and `LastName` columns. [cite: 4]
- **Schema Selection:** Filters and reorders columns for an optimized analytical schema. [cite: 4]
- **Delta Loading:** Appends the results into a Delta table, with the table name passed as a **Base Parameter** from the pipeline. 



### Sample Parameterized Code
```python
# Parameters cell
table_name = "sales"

# Transformation and Load
df = spark.read.format("csv").option("header","true").load("Files/new_data/*.csv")
df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))
df.write.format("delta").mode("append").saveAsTable(table_name)