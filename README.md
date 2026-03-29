# 🌍 Global Earthquake Data Pipeline (Medallion Architecture)

An automated end-to-end data engineering pipeline built on **Databricks** and **Delta Lake**. This project demonstrates a production-grade ETL process that ingests real-time seismic data from the USGS API and transforms it into clean, actionable insights using the **Medallion Architecture**.

## 🏗️ Architecture Overview
The pipeline follows the **Medallion (Multi-Hop) Architecture** to ensure data reliability and quality at every stage:

1.  **Bronze (Raw Layer):** * **Source:** USGS Earthquake API (GeoJSON).
    * **Mode:** `Append`.
    * **Role:** Acts as the landing zone for raw, immutable JSON data.
2.  **Silver (Cleaned Layer):** * **Logic:** **Idempotent Upsert (MERGE)**.
    * **Processing:** Flattening complex JSON, schema enforcement, and deduplication based on unique earthquake IDs.
3.  **Gold (Business Layer):** * **Mode:** `Overwrite`.
    * **Role:** Final, human-readable table with formatted timestamps (`event_time`) and metadata (`processed_at`), ready for BI tools.

---

## 🛠️ Tech Stack & Key Concepts
* **Engine:** PySpark (Spark SQL & DataFrames).
* **Storage:** Delta Lake (Supporting ACID transactions and MERGE operations).
* **Orchestration:** Databricks Jobs.
* **Idempotency:** The pipeline is designed to be run multiple times without creating duplicate records, ensuring a single source of truth.

---

## 💡 Engineering Challenges Solved
* **Duplicate Management:** Solved the "Double Ingestion" issue by implementing a `DeltaTable` MERGE logic instead of a simple append.
* **Schema Evolution:** Handled changes in the raw API response using `overwriteSchema` and explicit PySpark `StructType` definitions.
* **Time Normalization:** Converted Unix Epoch timestamps (milliseconds) into standard UTC formats for easier analysis.

---

## 🚀 How to Run
1.  Clone this repository.
2.  Import the provided Notebook into your **Databricks** workspace.
3.  Run the cells sequentially or schedule the Notebook as a **Databricks Job** (e.g., Hourly).

---

## 📈 Next Steps
- [ ] Connect **Databricks SQL Warehouse** to visualize earthquake hotspots on a map.
- [ ] Integrate **Apache Airflow** for cross-platform orchestration.
- [ ] Add automated Data Quality alerts (e.g., notify on Magnitude > 6.0).

---
**Project by:** [Abobakar Suliman]  
**Location:** Dubai, UAE  
**Role:** Cloud-Native Data Engineer
