# 🧪 Data Science: Training and Comparing Machine Learning Models

## Overview
This project explores the **Data Science** capabilities of Microsoft Fabric. It demonstrates a complete machine learning workflow: from ingesting open datasets and performing exploratory data analysis (EDA) to feature engineering with **Data Wrangler** and tracking experiments using **MLflow**.

## 🎯 Project Objectives
- [cite_start]Ingest the Azure Open Datasets **diabetes dataset** into a Spark DataFrame.
- [cite_start]Perform EDA using built-in **charting tools** to visualize data distributions.
- [cite_start]Use **Data Wrangler** to perform low-code data cleaning and generate Python code.
- [cite_start]Train and compare **Regression** (Linear Regression) and **Classification** (Logistic Regression) models.
- [cite_start]Log model parameters, metrics, and artifacts automatically with **MLflow**.
- [cite_start]Register the best-performing model in the Fabric **Model Registry**.

## 🛠️ Data Science Workflow

### 1. Exploratory Data Analysis (EDA)
[cite_start]Data was loaded from Azure Open Storage and converted into a Pandas DataFrame for compatibility with standard data science libraries. [cite_start]Initial analysis included using **Box Plots** to understand the distribution of the target variable `Y`.

### 2. Feature Engineering with Data Wrangler
To simplify the training process, I used **Data Wrangler**—a tool optimized for Pandas DataFrames—to:
- [cite_start]Analyze histograms and percentiles.
- [cite_start]Create a binary **Risk** column using a threshold (75th percentile of `Y`) to convert the problem into a classification task.
- [cite_start]Automatically generate and commit the transformation code back to the notebook.



### 3. Experiment Tracking with MLflow
I created two distinct MLflow experiments to track different modeling approaches:
- [cite_start]**`diabetes-regression`**: Focused on predicting the exact numerical value of diabetes progression (`Y`).
- [cite_start]**`diabetes-classification`**: Focused on predicting "Low Risk" vs. "High Risk" (`Risk`).

## 💻 Machine Learning Code Highlights

### Automated Logging with MLflow


## ⚙️ Key Skills Demonstrated

* **Advanced Feature Engineering:** Using Data Wrangler to derive insights and transform data types.
* **Experiment Orchestration:** Managing multiple ML runs and comparing metrics like **Accuracy** vs. **R-Squared**.
* **Model Management:** Saving and versioning models within the Fabric ecosystem for later deployment.
