# ⚡ Real-Time Intelligence: Ingesting and Analyzing Live Streams

## Overview
This project demonstrates the end-to-end flow of real-time data in **Microsoft Fabric**. It covers the ingestion of live stock market data through **Eventstreams**, storage in an **Eventhouse (KQL Database)**, and the creation of live visualizations and automated alerts using **Activator**.

## 🎯 Project Objectives
- Ingest live data using the **Fabric Real-Time Hub** and **Eventstreams**.
- Architect a **KQL Database** within an **Eventhouse** for high-velocity data storage.
- Perform real-time analytics using **Kusto Query Language (KQL)**.
- Build a **Real-Time Dashboard** with live-updating visualizations.
- Configure an **Activator alert** to trigger actions based on specific data patterns.

## 🛠️ Real-Time Architecture
The solution follows a streamlined path from source to action:

1.  [cite_start]**Source:** A live Stock Market sample stream.
2.  [cite_start]**Ingestion:** An **Eventstream** (`stock-data`) captures the incoming JSON events.
3.  [cite_start]**Storage:** The stream is connected to an **Eventhouse** table (`stock`) within a KQL database[cite: 6, 7].
4.  [cite_start]**Action:** A **Real-Time Dashboard** visualizes the data, and an **Activator** monitors for price changes[cite: 8, 9].



## 💻 KQL Analytics
I utilized **Kusto Query Language (KQL)** to perform temporal window aggregations on the live data.

### Average Price per Symbol (Last 5 Minutes)

stock
| where ["time"] > ago(5m)
| summarize avgPrice = avg(todecimal(bidPrice)) by symbol
| project symbol, avgPrice


## 🔔 Automated Alerts with Activator

To demonstrate the "**Intelligence**" aspect of Fabric, I implemented an **Activator** alert:

* **Condition:** Monitors the `avgPrice` of stock symbols.
* **Trigger:** Detects when a price **increases by 100 within a 5-minute window**.
* **Action:** Sends an automated **email notification** to the stakeholder.



## ⚙️ Key Skills Demonstrated

* **Live Stream Ingestion:** Connecting and managing continuous data sources.
* **KQL Proficiency:** Writing high-performance queries for time-series data.
* **Proactive Monitoring:** Using **Activator** to turn data insights into immediate actions.
* **Dashboarding:** Transitioning from raw data tables to live visual column charts.