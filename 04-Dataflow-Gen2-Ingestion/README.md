# 💧 Data Ingestion with Dataflow (Gen2) and Power Query

## Overview
This project demonstrates the use of **Dataflow (Gen2)** in Microsoft Fabric to ingest and transform data using a low-code interface. The lab highlights the integration of **Power Query** for complex data transformations and the orchestration of these dataflows within **Fabric Pipelines**.

## 🎯 Project Objectives
- Create a **Dataflow (Gen2)** to extract data from an external CSV source.
- Utilize **Power Query** to perform data transformations, including adding custom columns.
- Configure a **Lakehouse destination** for the transformed data.
- Orchestrate the dataflow using a **Fabric Data Pipeline**.

## 🛠️ ETL Process with Power Query
The data transformation logic was built visually using the Power Query editor:

1.  **Data Extraction:** Connected to an external `orders.csv` file via an HTTP connection.
2.  **Custom Column Creation:** Added a new column `MonthNo` using the Power Query M formula: `Date.Month([OrderDate])`.
3.  **Data Typing:** Verified and enforced data types (e.g., `Date` for `OrderDate` and `Whole Number` for `MonthNo`) to ensure downstream data quality.
4.  **Destination Mapping:** Directed the output to a new `orders` table within the Lakehouse, using the **Append** update method.



## 🚀 Pipeline Orchestration
To automate the ingestion process, the Dataflow was embedded into a **Fabric Data Pipeline**:
- **Activity:** Added a "Dataflow" activity to a pipeline named `Load data`.
- **Configuration:** Linked the activity to `Dataflow 1` and executed it to populate the Lakehouse tables.
- **Verification:** Refreshed the Lakehouse explorer to confirm the successful creation and population of the `orders` table.

## ⚙️ Key Skills Demonstrated
- **Low-Code ETL:** Building complex data movements without writing extensive code.
- **Power Query (M):** Applying functional transformations to raw datasets.
- **Hybrid Orchestration:** Combining visual dataflows with structured pipeline activities for a complete end-to-end process.

## 🔗 Learning Resource
This implementation is based on the official Microsoft Fabric documentation:
- **Lab:** [Create a Dataflow (Gen2) to ingest data](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/02-dataflow-gen2.html)