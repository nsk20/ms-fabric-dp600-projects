# 📊 Microsoft Fabric Lakehouse Implementation (DP-600 Certification Preparation)

## Overview

This project documents the successful completion of a foundational data engineering lab focused on implementing a **Microsoft Fabric Lakehouse**. This hands-on exercise was completed as part of preparation for the **Microsoft Certified: Fabric Analytics Engineer (DP-600)** certification.

The primary objective was to demonstrate proficiency in core Fabric components by ingesting raw data, transforming it into a structured Delta Lake table, and performing analytical queries.

## 🎯 Project Goal

To establish a complete data analytics environment within Microsoft Fabric's unified platform, specifically:
1.  Set up a new Fabric workspace and a Lakehouse artifact.
2.  Ingest raw CSV data into the Lakehouse's raw storage (`Files` layer).
3.  Load the raw file data into a structured **Delta Lake table** (`Tables` layer).
4.  Query and analyze the data using both the **SQL Analytics Endpoint** and **Visual Query (Power Query)**.

## 🛠️ Key Technologies & Concepts

| Category | Tool / Concept | Description |
| :--- | :--- | :--- |
| **Platform** | **Microsoft Fabric** | The all-in-one analytics solution for enterprises. |
| **Data Architecture** | **Lakehouse** | A unified data storage architecture combining the flexibility of a data lake with the structure of a data warehouse. |
| **Table Format** | **Delta Lake** | The underlying open-source storage format used for managed tables in Fabric, providing ACID properties and schema enforcement. |
| **Querying** | **SQL Analytics Endpoint** | Enables querying of Delta tables using standard T-SQL semantics. |
| **Transformation** | **Visual Query (Power Query)** | Used to perform no-code data transformations and aggregations. |

## ⚙️ Steps Completed

The following core data engineering tasks were executed:

1.  **Workspace & Lakehouse Creation:** Created a new Microsoft Fabric workspace and provisioned a new Lakehouse artifact.
2.  **Data Ingestion:** Uploaded a raw `sales.csv` file into the `/Files/data` folder of the Lakehouse's OneLake storage.
3.  **Table Creation (Load to Tables):** Loaded the raw CSV file into a new managed table named `sales`, automatically converting the data into the **Delta Lake** format.
4.  **SQL Analysis:** Connected to the default **SQL Analytics Endpoint** and executed a T-SQL query to calculate key metrics.
5.  **Visual Query:** Used the Power Query interface to create a visual transformation, counting distinct line items per sales order.

## 💻 SQL Analysis Example

To demonstrate analytical capabilities, the following T-SQL query was executed against the newly created Delta table:

```sql
SELECT 
    Item, 
    SUM(Quantity * UnitPrice) AS Revenue 
FROM 
    sales 
GROUP BY 
    Item 
ORDER BY 
    Revenue DESC;
