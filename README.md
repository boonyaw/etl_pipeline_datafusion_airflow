# ETL Project with Data Fusion, Airflow, and BigQuery

This repository contains code and configuration files for an **Extract, Transform, Load (ETL)** pipeline using:

- 🧪 **Google Cloud Data Fusion** (for data extraction and transformation)
- 🔄 **Apache Airflow / Cloud Composer** (for orchestration)
- 📊 **Google BigQuery** (for data loading and analytics)

---

## 📝 Project Overview

This project performs the following key tasks:

### ✅ Data Extraction
- Extract raw data using Python (e.g. from a REST API or flat files).

### 🔐 Data Masking
- Apply data masking and encoding to sensitive fields in **Cloud Data Fusion** before storing.

### 📥 Data Loading
- Load clean, transformed data into **Google BigQuery** tables.

### 🛠️ Orchestration
- Automate the complete data pipeline using **Apache Airflow** via **Google Cloud Composer**.

---
## 🚀 How to Run This Project (Simplified Steps)

### 1. Set Up GCP Services

- Create a project on **Google Cloud Console**
- Enable the following APIs:
  - Cloud Data Fusion
  - BigQuery
  - Cloud Composer
  - Cloud Storage
- Create:
  - A **Cloud Storage bucket** (to hold input data and DAG files)
  - A **BigQuery dataset** (for storing transformed data)
  - A **Cloud Composer environment** (Airflow)

---

### 2. Deploy Cloud Data Fusion Pipeline

- Use the Cloud Data Fusion UI to create a new pipeline
- Data flow:
  - **Source:** GCS (CSV file generated via Python)
  - **Transformation:** Use Wrangler to mask and clean sensitive fields
  - **Sink:** BigQuery table
- Save and deploy the pipeline
- Manually test once to ensure it loads sample data into BigQuery

---

### 3. Upload Airflow DAGs (Cloud Composer)

- Inside your GCS bucket (auto-created by Composer), locate the `/dags` folder
- Upload your custom **Airflow DAG `.py` file**
- Also upload your `extract.py` script into a `/scripts` subfolder if needed
- DAG will auto-appear in the Composer UI within 1–2 minutes

---

### 4. Monitor Jobs in Cloud Composer

- Open Airflow UI from Composer
- View your DAG (e.g. `employee_data_etl`)
- Trigger it manually or wait for schedule
- Monitor:
  - Logs of each task
  - Task status: success, failure, retries
- Use task dependencies to ensure sequential execution (e.g. `extract_data >> start_pipeline`)

---

### 5. View Results in BigQuery

- Open your BigQuery dataset
- You should see the auto-created table (e.g. `employee_data`)
- View and query the transformed records
- (Optional) Connect to **Looker Studio** to visualize the final data on dashboards

---

✅ Once all steps are completed, your pipeline will:
1. Generate & extract data via Python
2. Load it into Cloud Storage
3. Transform + mask it in Data Fusion
4. Load into BigQuery
5. Automate the entire flow via Airflow DAGs

