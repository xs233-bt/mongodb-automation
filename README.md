# 📦 MongoDB Device Orders ETL Pipeline

An end-to-end ETL pipeline that automatically extracts order data from MongoDB Atlas, transforms nested documents into structured business datasets, detects refunds incrementally, generates formatted Excel reports, and delivers them to OneDrive.

The pipeline is fully automated using Apache Airflow and is designed for daily production reporting.

---

# Architecture
<img width="1039" height="627" alt="image" src="https://github.com/user-attachments/assets/fd2368df-4387-40eb-a938-e93a4c46352f" />



---

# Project Overview

This project was built to automate daily operational reporting by transforming semi-structured MongoDB data into business-ready Excel reports.

The workflow performs the following tasks automatically:

- Connects to MongoDB Atlas
- Executes MongoDB Aggregation Pipeline
- Extracts aggregated documents using PyMongo
- Cleans and transforms data using Pandas
- Detects newly refunded orders
- Maintains historical refund records
- Generates formatted Excel reports
- Saves outputs to OneDrive
- Runs automatically every day using Apache Airflow

The pipeline eliminates manual report generation while improving reporting consistency and accuracy.

---

# Key Features

## Automated Scheduling

The workflow is orchestrated using Apache Airflow.

Features include:

- Daily scheduled execution
- Automatic retry
- Logging
- Task monitoring
- Failure recovery

---

## MongoDB Aggregation

Instead of loading raw nested documents into Python, MongoDB performs most heavy transformations.

Aggregation includes:

- Flatten nested arrays
- Match required products
- Convert timestamps
- Join Contact Profiles
- Add Channel and Customer fields
- Sort and project final output

This reduces network traffic and improves overall pipeline performance.

---

## Data Extraction

Technology:

- PyMongo

Responsibilities:

- Connect to MongoDB Atlas
- Execute aggregation pipeline
- Load aggregated results
- Convert documents into Pandas DataFrame

---

## Data Transformation

Technology:

- Pandas

Processing includes:

- Remove invalid records
- Convert Unix timestamps
- Standardize datetime format
- PST timezone conversion
- Rename columns
- Business logic mapping
- Product normalization
- Data validation

The output becomes a clean structured dataset suitable for reporting.

---

## Refund Detection

One of the major features of the project.

Pipeline automatically compares today's data with yesterday's snapshot.

Workflow:

Yesterday Snapshot

↓

Today's Orders

↓

Compare Order Status

↓

Detect Newly Refunded Orders

↓

Append Refund History

↓

Save refund_history.csv

Features:

- Incremental processing
- Duplicate prevention
- Persistent refund history
- Idempotent execution

---

## Excel Report Generation

Technology:

- OpenPyXL

Automatically generates a formatted Excel workbook containing:

### Order Summary

- Daily Units
- MTD Units
- YTD Units

### Orders by Product

- Product breakdown
- Units
- Totals

### Refund Summary

- Newly refunded orders
- Refund counts

### Source Data

Complete cleaned dataset used for reporting.

Formatting includes:

- Currency formatting
- Totals
- Borders
- Auto column width
- Header styling

---

## Output Storage

Generated reports are automatically saved to OneDrive.

Outputs include:

device_orders_YYYY-MM-DD.xlsx

refund_history.csv

This allows business users to access reports without manual intervention.

---

# Pipeline Flow

```text
MongoDB Atlas
        │
        ▼
MongoDB Aggregation Pipeline
        │
        ▼
Apache Airflow
        │
        ▼
PyMongo Extraction
        │
        ▼
Pandas Transformation
        │
        ▼
Refund Detection
        │
        ▼
Excel Generation
        │
        ▼
OneDrive
```

---

# Technologies

| Category | Technology |
|------------|------------|
| Language | Python |
| Database | MongoDB Atlas |
| Workflow | Apache Airflow |
| Driver | PyMongo |
| Data Processing | Pandas |
| Reporting | OpenPyXL |
| Storage | OneDrive |
| Version Control | Git |

---

# Project Structure

```
project/

│

├── dags/
│     device_orders_generate.py
│
├── scripts/
│     extract.py
│     transform.py
│     refund.py
│     report.py
│
├── output/
│     device_orders_YYYY-MM-DD.xlsx
│     refund_history.csv
│
├── config/
│
├── requirements.txt
│
└── README.md
```

---

# Data Flow

```
Raw MongoDB Documents

↓

MongoDB Aggregation

↓

Aggregated Documents

↓

Pandas Cleaning

↓

Business Dataset

↓

Refund Detection

↓

Excel Report

↓

OneDrive
```

---

# Business Value

This pipeline provides significant operational improvements.

### Automation

- Eliminates manual report generation

### Accuracy

- Consistent business logic
- Standardized calculations

### Visibility

Provides

- Daily Orders
- MTD Orders
- YTD Orders
- Product Breakdown
- Refund Tracking

### Reliability

- Retry mechanism
- Incremental processing
- Duplicate prevention

### Scalability

The architecture can easily support additional reports and new MongoDB collections.

---

# Engineering Highlights

This project demonstrates several Data Engineering concepts.

✔ ETL Pipeline Design

✔ MongoDB Aggregation Framework

✔ Apache Airflow Orchestration

✔ Incremental Processing

✔ Idempotent Workflow

✔ Business Data Transformation

✔ Automated Reporting

✔ Production Scheduling

✔ Historical Data Tracking

✔ End-to-End Automation

---

# Future Improvements

Potential enhancements include:

- Azure Data Lake Storage
- Azure Synapse Pipeline
- Databricks
- Parquet Output
- Delta Lake
- Power BI DirectLake
- Automated Email Distribution
- Data Quality Validation
- Great Expectations
- CI/CD Deployment
- Docker Containerization
- Cloud Deployment (Azure)

---

# Example Output

```
device_orders_2026-07-14.xlsx

├── Order Summary
├── Orders by Product
├── Refund Summary
└── Source Data
```

---

# Skills Demonstrated

- Python
- MongoDB
- MongoDB Aggregation Pipeline
- Apache Airflow
- PyMongo
- Pandas
- OpenPyXL
- ETL Design
- Workflow Automation
- Data Transformation
- Incremental Data Processing
- Excel Automation
- Business Reporting
- Production Scheduling
