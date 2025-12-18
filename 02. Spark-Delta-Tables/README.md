# 🚀 Use Delta Tables in Apache Spark (DP-600)

## Overview
This project focuses on advanced data engineering within **Microsoft Fabric** using **Apache Spark**. [cite_start]The lab demonstrates how to manage, version, and query data using the open-source **Delta Lake** format, which provides relational semantics for big data[cite: 457, 458].

## 🎯 Project Objectives
- [cite_start]Ingest and explore data using **PySpark DataFrames**[cite: 528].
- [cite_start]Implement and compare **Managed** vs. **External** Delta tables[cite: 610].
- [cite_start]Perform data updates and manage **Table Versioning (Time Travel)**[cite: 696, 698].
- [cite_start]Utilize **Spark Structured Streaming** to sink live data into Delta tables[cite: 780].

## 🛠️ Technical Implementation

### 1. Managed vs. External Tables
I implemented both table types to understand Fabric's metadata management:
- [cite_start]**Managed Tables:** Fabric manages both the schema metadata and the data files in the `Tables` folder[cite: 611].
- [cite_start]**External Tables:** Data files are stored in a custom location (e.g., the `Files` folder), while Fabric only manages the metadata[cite: 612, 626].

### 2. Time Travel & Versioning
[cite_start]Using the `DESCRIBE HISTORY` command, I explored the transaction log stored in JSON format within the `_delta_log` folder[cite: 697, 709].
- [cite_start]**Data Update:** Applied a 10% price reduction to specific categories using Spark SQL[cite: 699, 702].
- [cite_start]**Versioning:** Successfully queried the "Version 0" (original) data even after updates were committed, demonstrating Delta Lake's historical data retention[cite: 724, 725].

### 3. Real-Time Streaming
I simulated an **IoT scenario** by creating a streaming source:
- [cite_start]Read JSON event data from a folder using a defined schema[cite: 796, 797].
- [cite_start]Used a Delta table as a **streaming sink** with checkpointing to ensure data consistency[cite: 781, 822].
- [cite_start]Demonstrated that the Delta table automatically updates as new files are added to the source stream[cite: 856].

## 💻 Code Highlights

### Schema Definition & Data Loading
```python
from pyspark.sql.types import StructType, IntegerType, StringType, DoubleType

# Define schema for raw CSV ingestion
schema = StructType() \
    .add("ProductID", IntegerType(), True) \
    .add("ProductName", StringType(), True) \
    .add("Category", StringType(), True) \
    .add("ListPrice", DoubleType(), True)

df = spark.read.format("csv").option("header","true").schema(schema).load("Files/products/products.csv")
display(df)
[cite_start]``` [cite: 562, 572]

### Time Travel Query
```python
# Accessing original data version using Time Travel
original_data = spark.read.format("delta").option("versionAsOf", 0).load('Files/external_products')
display(original_data)
[cite_start]``` [cite: 720, 725]

## 🔗 Learning Resource
This implementation is based on the official Microsoft Learning course for Fabric Analytics Engineers:
- [cite_start]**Lab:** [Use Delta Tables in Apache Spark](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/03-delta-lake.html) [cite: 436]