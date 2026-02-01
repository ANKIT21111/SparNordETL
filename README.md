# 🏦 Spar Nord Bank: ATM Withdrawal Behavior & ETL Analytics 🚀

![Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Redshift](https://img.shields.io/badge/Amazon_Redshift-8C4FFF?style=for-the-badge&logo=amazon-redshift&logoColor=white)

## 📖 Project Overview
Spar Nord Bank, a leading Danish financial institution, sought to optimize its ATM replenishment strategy. This project involved building a robust **End-to-End ETL Pipeline** to process over **2.4 million transaction records**, correlated with real-time weather data, to identify patterns in withdrawal behavior.

### 🎯 Business Objective
To analyze the impact of temporal, locational, and environmental factors (weather) on ATM usage, enabling the bank to:
- 📉 Reduce operational costs by optimizing refill frequency.
- 💳 Ensure high ATM availability during peak demand periods.
- 🌦️ Understand how weather conditions affect withdrawal volumes.

---

## 🛠️ Tech Stack & Tools
| Category | Technologies |
| :--- | :--- |
| **Big Data Engine** | Apache Spark (PySpark) |
| **Data Ingestion** | Apache Sqoop, HDFS |
| **Cloud Infrastructure** | AWS S3, AWS Redshift, AWS EMR (EC2) |
| **Languages** | Python, SQL |
| **Data Modeling** | Star Schema (Dimensional Modeling) |

---

## 🏗️ Data Pipeline Architecture

1.  **Ingestion**: Leveraged **Apache Sqoop** to ingest raw transactional data from an RDS MySQL database into **HDFS**.
2.  **Processing (ETL)**: Used **PySpark** to:
    -   Perform complex data cleaning and schema enforcement.
    -   Join transactional data with environmental weather datasets.
    -   Transform flat data into a optimized **Star Schema**.
3.  **Storage**: Exported processed dimensions and facts to **AWS S3** in optimized CSV/Parquet formats.
4.  **Warehousing**: Loaded the finalized dimensional model into **Amazon Redshift** for high-performance analytical querying.

---

## 📊 Target Dimensional Model (Star Schema)

The architecture is built around a centralized Fact table connected to optimized Dimension tables.

### 1. 📍 DIM_LOCATION
*Captures granular geographical details of ATM placements.*
- `location_id` (PK), `location_name`, `street_name`, `zipcode`, `latitude`, `longitude`.

### 🏧 2. DIM_ATM
*Details regarding ATM hardware and status.*
- `atm_id` (PK), `atm_number`, `manufacturer`, `location_id` (FK).

### 📅 3. DIM_DATE
*Enables temporal analysis across hours, days, and seasons.*
- `date_id` (PK), `full_timestamp`, `year`, `month`, `day`, `weekday`, `hour`.

### 💳 4. DIM_CARD_TYPE
*Categorizes transactions by card issuer.*
- `card_type_id` (PK), `card_type`.

### 💰 5. FACT_ATM_TRANS
*The core metrics table containing millions of rows of transaction and weather data.*
- `trans_id` (PK), `atm_id`, `location_id`, `date_id`, `card_type_id`, `amount`, `weather_id`, `temp`, `pressure`, `humidity`, etc.

---

## 📈 Analytical Capabilities
With this pipeline, recruiters and analysts can answer critical questions:
- **Peak Hour Analysis**: *"Which weekdays see the highest withdrawal volume between 5 PM and 8 PM?"*
- **Weather Impact**: *"Do customers withdraw more cash during rainy weather compared to sunny days?"*
- **Location Performance**: *"Which zip codes exhibit the highest ATM 'Inactive' status frequency?"*
- **Manufacturer Reliability**: *"Which ATM manufacturer (NCR vs. Diebold) has fewer error messages?"*

---

## 📁 Project Structure
```bash
├── SparkNordBank_SparkETLCode.py.ipynb  # Core ETL Logic (PySpark)
├── SqoopDataIngestion.pdf               # Ingestion Configuration Details
├── RedshiftSetup.pdf                    # Warehouse Configuration
├── Redshift Analytical Queries.pdf       # SQL Insights & Reporting
└── README.md                            # Project Documentation
```

---

## 🚀 Key Takeaways
- Successfully handled **large-scale data processing** using Spark's distributed computing.
- Implemented **Industry-Standard Dimensional Modeling** to ensure fast query performance in Redshift.
- Integrated **disparate datasets** (Banking + Weather) to provide 360-degree business insights.

---
**Developed by [Ankit Abhishek]** 👨‍💻
*Passionate about building scalable data solutions and driving business value through analytics.*
