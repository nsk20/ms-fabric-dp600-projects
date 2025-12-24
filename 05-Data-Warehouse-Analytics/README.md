# 🏛️ Data Warehouse Implementation and Analysis in Microsoft Fabric

## Overview
This project demonstrates the creation and management of a **Microsoft Fabric Data Warehouse**. Unlike Lakehouse SQL endpoints, the Fabric Warehouse provides a full relational database experience with support for **Data Manipulation Language (DML)** operations (Insert, Update, Delete) and robust multi-table modeling.

## 🎯 Project Objectives
- Architect a relational data warehouse using **T-SQL** to define schemas and tables.
- Implement a **Star Schema** consisting of Fact and Dimension tables.
- Perform advanced analytical querying using **JOINs** and **Aggregations**.
- Develop reusable database objects including **Views**.
- Utilize **Visual Queries** for no-code data exploration and filtering.
- (Optional) Design a **Semantic Model** to define relationships for Power BI reporting.

## 🏗️ Data Warehouse Architecture
I implemented a classic star schema designed for sales analysis. This architecture optimizes query performance by separating business process metrics (Facts) from descriptive attributes (Dimensions).



### The Schema Includes:
- **FactSalesOrder:** Contains numeric measures like `SalesTotal`.
- **DimProduct / DimCustomer / DimDate:** Provide context for analysis (Product names, Customer regions, and Time hierarchies).

## 💻 SQL Development Highlights

### 1. Table Creation and Data Ingestion
I used standard T-SQL to define entities and populate them, demonstrating the Warehouse's ability to handle traditional relational database tasks.

CREATE TABLE dbo.DimProduct (
    ProductKey INTEGER NOT NULL,
    ProductName VARCHAR(50) NOT NULL,
    Category VARCHAR(50) NULL,
    ListPrice DECIMAL(5,2) NULL
);

INSERT INTO dbo.DimProduct VALUES (1, 'RING1', 'Bicycle bell', 'Accessories', 5.99);


### 2. Analytical Querying and Views
I developed complex queries to aggregate sales revenue across multiple dimensions and encapsulated this logic into a View for simplified reporting.

CREATE VIEW vSalesByRegion AS
SELECT  
    d.[Year] AS CalendarYear,
    c.CountryRegion AS SalesRegion,
    SUM(so.SalesTotal) AS SalesRevenue
FROM FactSalesOrder AS so
JOIN DimDate AS d ON so.SalesOrderDateKey = d.DateKey
JOIN DimCustomer AS c ON so.CustomerKey = c.CustomerKey
GROUP BY d.[Year], c.CountryRegion;


## 🖱️ Visual Query Experience
For rapid analysis without code, I utilized the **Visual Query Designer** to perform the following:

* **Merge Queries:** Joined `FactSalesOrder` with `DimProduct` using a graphical interface to consolidate relational data.
* **Filter Data:** Isolated specific product performance (e.g., "Cable Lock" data) to answer immediate business requests with high precision.

---

## ⚙️ Key Skills Demonstrated
* **Full SQL Semantics:** Implementing Data Definition Language (DDL) and Data Manipulation Language (DML) operations.
* **Data Modeling:** Creating many-to-one relationships to build a robust and functional semantic model.
* **Business Intelligence Logic:** Designing views to standardize organizational metrics and ensure a "single source of truth."