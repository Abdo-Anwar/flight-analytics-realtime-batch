# 🛫 Flight Performance & Delay Decision System

## **Project Overview**

This project is a **full-fledged aviation analytics system** designed to empower airlines, airport operators, and stakeholders to monitor, analyze, and act on flight delays, cancellations, and operational bottlenecks. It combines **batch processing for historical data** and **streaming analytics for real-time monitoring**, bridging the gap between raw flight data and actionable insights.

### **Business Motivation**

The aviation industry is one of the largest and most data-intensive sectors globally:

* **Trillions of dollars in revenue**, with **millions of daily flights**
* Operational challenges: delays, cancellations, gate congestion, taxi-outs
* High cost per minute of delay (>$100/minute) and average flight delays (~13 mins)
* Decision-making relies on delayed reports (hours to days), leading to inefficient responses

**Our solution:** A pipeline that **integrates historical and live flight data** to detect anomalies, calculate KPIs, and deliver insights that **directly support operational and strategic decisions**.

---

## **Key Objectives**

* Build a **scalable, end-to-end data platform**
* Process **~7M historical flight records (35 columns)** in batch
* Stream **real-time flight events** (delays, cancellations, diversions)
* Generate **clean dimensional models** for analytics and ML
* Deliver **interactive dashboards** (Power BI for batch, Grafana for streaming)

---

## **Table of Contents**

1. [Data Source & Dictionary](#data-source--dictionary)
2. [System Architecture](#system-architecture)
3. [Batch Pipeline](#batch-pipeline)
4. [Streaming Pipeline](#streaming-pipeline)
5. [Data Modeling & dbt](#data-modeling--dbt)
6. [Dashboards & KPIs](#dashboards--kpis)
7. [How to Run](#how-to-run)
8. [Code Snippets](#code-snippets)
9. [Business Insights](#business-insights)
10. [Author & License](#author--license)

---

## **Data Source & Dictionary**

* **Dataset:** BTS TranStats Flight On-Time Performance (2024)
* **Records:** >7M, **Columns:** 35
* **Use Cases:** Flight delay analysis, cancellation patterns, airline performance, airport congestion, and route optimization.

**Data Dictionary (sample):**

| Column            | Description                   |
| ----------------- | ----------------------------- |
| `fl_date`         | Flight date (YYYY-MM-DD)      |
| `dep_delay`       | Departure delay in minutes    |
| `arr_delay`       | Arrival delay in minutes      |
| `carrier_delay`   | Delay due to carrier          |
| `weather_delay`   | Delay due to weather          |
| `nas_delay`       | National Air System delay     |
| `cancelled`       | Flight cancellation indicator |
| `origin` / `dest` | Airport codes                 |
| …                 | …                             |

> Full dictionary in `/docs/data_dictionary.md`

**Dataset Link:** [Flight Data 2024 - Kaggle](https://www.kaggle.com/datasets/hrishitpatil/flight-data-2024)

---

## **System Architecture**

![System Architecture](images/data_platform_flight.png)

### **Overview**

The system contains **two parallel pipelines**:

1. **Batch / Historical Pipeline** (for AI/analytics)

   * Source: MySQL with **Change Data Capture (CDC)**
   * Flow: `MySQL CDC → S3 → Snowflake → dbt → Power BI`
   * Features: Cost-efficient storage, batch analytics, machine learning support

2. **Real-Time Streaming Pipeline** (for monitoring and anomaly detection)

   * Source: MySQL CDC → **Flink**
   * Flow: `MySQL CDC → Flink → Postgres → Grafana`
   * Features: Real-time dashboards, alerting, operational insights

---

## **Batch Pipeline**

* **Tools:** Python, Spark Structured Streaming, Airflow, S3, Snowflake, Power BI
* **Process:**

  1. Ingest CSVs into **MySQL**
  2. CDC captures changes and streams to **Kafka**
  3. Spark jobs read from Kafka, transform, and write to **S3**
  4. Snowflake pulls cleaned data from S3
  5. **dbt** builds dimensional models for analytics
  6. Power BI dashboards visualize business KPIs

**Code placeholder:**

```python
# INSERT spark consumer.py / batch transformation snippet here
```

---

## **Streaming Pipeline**

* **Tools:** Flink, Postgres, Kafka, Grafana
* **Features:**

  * Monitor **high-delay routes**, cancellations, and taxi-out congestion
  * Detect **real-time anomalies** and trigger alerts
  * Track **flight volume & delay trends** every 30 seconds

**Code placeholder:**

```python
# INSERT Flink streaming transformation example here
```

---

## **Data Modeling & dbt**

* **Star-schema design** for fast queries
* **Fact Table:** `fact_flights` (delays, cancellations, flight duration, distance)
* **Dimensions:** `dim_airline`, `dim_airport`, `dim_date`, `dim_route`
* dbt handles **transformations, testing, and lineage tracking**

**Data Lineage:**
![Data Lineage](images/data_lineage_flight.jpeg)

---

## **Dashboards & KPIs**

### **Batch (Power BI)**

* Airline performance & operational KPIs
* Regional & state analysis
* Executive overview & strategic decision support

### **Streaming (Grafana)**

* High-delay route monitor
* Real-time cancellation spikes
* Departure congestion (Taxi-Out Analysis)
* Delay trend time-series

![Example Dashboard](images/frist.png)

**Video Demos:**

* [Batch Pipeline Demo](https://drive.google.com/file/d/12c-LKxtjz0Ec_E_pWlF4yNFMsS0A9Ftn/view?usp=sharing)
* [Streaming Pipeline Demo](https://drive.google.com/file/d/1nOydJw4a6fAl49vQyVWYmv6L1MYq_Tg6/view?usp=sharing)

---

## **How to Run**

1. Start Docker containers

```bash
docker compose up -d
```

2. Access services:

   * Power BI: `<your_powerbi_url>`
   * Grafana: `<your_grafana_url>`
3. Run batch DAG via Airflow

```bash
python sparkJops/import_mysql.py
```

4. Start streaming job via Flink

```bash
docker compose exec flink-jobmanager flink run /opt/flink_jobs/streaming_job.py
```

**Note:** Replace credentials, S3 paths, Snowflake configuration, and access keys with your environment variables.

---

## **Code Snippets Placeholder**

```sql
-- Example dbt model: fact_flights
{{ config(materialized='table') }}

SELECT 
    fl_date,
    carrier,
    origin,
    dest,
    dep_delay,
    arr_delay,
    cancelled,
    diverted
FROM {{ source('raw', 'flight_data') }}
WHERE cancelled = 0
```

```python
# Example Flink streaming transformation
from pyflink.datastream import StreamExecutionEnvironment
from pyflink.table import StreamTableEnvironment

env = StreamExecutionEnvironment.get_execution_environment()
t_env = StreamTableEnvironment.create(env)

# Define source table
t_env.execute_sql("""
    CREATE TABLE flight_events (
        flight_id STRING,
        event_time TIMESTAMP(3),
        delay_minutes INT,
        event_type STRING
    ) WITH (
        'connector' = 'kafka',
        'topic' = 'flight-updates',
        'properties.bootstrap.servers' = 'localhost:9092',
        'format' = 'json'
    )
""")
```

---

## **Business Insights**

* Immediate detection of delays and cancellations saves **millions in operational costs**
* Historical analysis helps **identify bottlenecks** and optimize **fleet utilization**
* Dashboards empower stakeholders from **tactical operations to executive-level strategic planning**

---

## **Author & License**

**Abdelrhman Anwar** – Big Data Engineer
📧 [abd.ahm.anwar@gmail.com](mailto:abd.ahm.anwar@gmail.com) | 🔗 [LinkedIn](https://www.linkedin.com/in/abdelrhman-anwar)

License: **Personal Use / Educational Purposes** – contact author for commercial use

---
