# 🌊 Houston Flood Data Pipeline

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-336791?logo=postgresql)
![Power%20BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-150458?logo=pandas)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-ORM-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

An end-to-end **Data Engineering** project that collects weather observations, transforms raw environmental data, stores structured datasets in **PostgreSQL**, and powers an interactive **Power BI dashboard** for monitoring flood risk across the Houston metropolitan area.

The project demonstrates how modern ETL pipelines convert raw weather information into actionable insights for emergency planning, flood monitoring, and data-driven decision making.

---

## 📅 Project Timeline

**June 20, 2026 – July 15, 2026**

---

# 📖 Overview

Houston experiences some of the most frequent flooding events in the United States due to:

* Heavy rainfall
* Flat topography
* Extensive bayou systems
* Rapid urban development
* Poor drainage during severe storms

Raw weather data alone provides limited value. This project transforms that information into meaningful flood-risk indicators through a complete ETL pipeline.

The pipeline continuously demonstrates the core responsibilities of a Data Engineer:

* Extracting external data
* Cleaning and transforming datasets
* Loading data into relational databases
* Supporting business intelligence dashboards
* Producing analytical insights

---

# 🎯 Objectives

* Build a complete ETL pipeline using Python
* Collect weather data from an external API
* Clean and standardize environmental data
* Store processed information in PostgreSQL
* Calculate flood-risk scores
* Visualize trends using Power BI
* Enable scalable reporting for flood monitoring

---

# ✨ Features

* 🌦️ Collects weather data from an external API
* 🧹 Cleans and transforms raw datasets
* 🗄️ Loads structured data into PostgreSQL
* 🌧️ Calculates flood-risk scores
* 📊 Generates Power BI dashboards
* 📍 Identifies high-risk Houston locations
* 🔄 Repeatable ETL workflow
* 📈 Historical weather trend analysis

---

# 🛠 Tech Stack

| Category              | Technologies          |
| --------------------- | --------------------- |
| Programming           | Python                |
| Database              | PostgreSQL            |
| Data Processing       | Pandas                |
| API Integration       | Requests              |
| ORM                   | SQLAlchemy / psycopg2 |
| Business Intelligence | Power BI              |
| Version Control       | Git & GitHub          |

---

# 🏗 System Architecture

```text
                Weather API
                     │
                     ▼
          Data Extraction (Python)
                     │
                     ▼
        Cleaning & Data Transformation
                     │
                     ▼
          PostgreSQL Data Warehouse
                     │
                     ▼
          Power BI Dashboard
                     │
                     ▼
        Houston Flood Risk Analytics
```

---

# 🔄 ETL Workflow

## 1️⃣ Extract

Weather observations are retrieved through an external weather API.

Collected attributes include:

* Temperature
* Humidity
* Rainfall
* Wind Speed
* Weather Conditions
* Precipitation Probability
* Geographic Location
* Observation Timestamp

---

## 2️⃣ Transform

The transformation layer prepares raw weather data for analytics.

Processing includes:

* Removing invalid records
* Handling missing values
* Formatting timestamps
* Standardizing location names
* Converting data types
* Aggregating rainfall
* Computing flood-risk categories

Example risk classifications:

```text
Low Risk
Moderate Risk
High Risk
Severe Risk
```

---

## 3️⃣ Load

Clean datasets are loaded into PostgreSQL for long-term storage and analytical querying.

Example tables:

```text
locations
weather_observations
flood_risk_scores
pipeline_logs
```

---

## 4️⃣ Visualize

Power BI connects directly to PostgreSQL to provide interactive dashboards including:

* Rainfall Trends
* Flood Risk by Area
* Weather Summaries
* High-Risk Locations
* Risk Score Distribution
* Time-Series Analysis

---

# 📊 Data Pipeline

```text
Weather API
     │
     ▼
Extract Weather Data
     │
     ▼
Transform & Clean Data
     │
     ▼
Generate Flood Risk Scores
     │
     ▼
Load into PostgreSQL
     │
     ▼
Power BI Dashboard
     │
     ▼
Flood Risk Insights
```

---

# 🗃 Database Schema

```sql
locations
-----------
location_id
location_name
zip_code
latitude
longitude

weather_observations
---------------------
observation_id
location_id
temperature
humidity
rainfall
wind_speed
precipitation_probability
weather_condition
observation_time

flood_risk_scores
------------------
risk_id
observation_id
risk_score
risk_level
created_at
```

---

# 🌧 Flood Risk Model

Flood risk is estimated using environmental indicators such as:

* Rainfall
* Humidity
* Precipitation Probability

Current scoring logic:

```text
Rainfall ≥ 3.0 in   → Severe Risk

Rainfall ≥ 2.0 in   → High Risk

Rainfall ≥ 1.0 in   → Moderate Risk

Rainfall < 1.0 in   → Low Risk
```

The scoring model is intentionally modular and can later incorporate:

* Bayou water levels
* River gauges
* Soil saturation
* Historical flooding records
* GIS mapping
* NOAA storm alerts

---

# 📈 Dashboard Highlights

The Power BI dashboard provides:

* 📍 Flood Risk by Houston Area
* 🌧 Rainfall Trends
* 📅 Daily Weather Activity
* 🚨 High-Risk Alerts
* 📊 Risk Distribution
* 🛰 Geographic Flood Monitoring

Example KPIs include:

* Average Rainfall
* Highest Risk Score
* Areas Under Severe Risk
* Daily Rainfall Totals
* Weather Condition Frequency

---

# 📂 Project Structure

```text
Houston-Flood-Data-Pipeline
│
├── config/
│   └── database_config.py
│
├── data/
│   ├── raw/
│   └── processed/
│
├── powerbi/
│   └── houston_flood_dashboard.pbix
│
├── scripts/
│   ├── extract_weather.py
│   ├── transform_weather.py
│   ├── load_to_postgres.py
│   └── run_pipeline.py
│
├── sql/
│   ├── create_tables.sql
│   └── sample_queries.sql
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

# 🚀 Getting Started

## Clone the Repository

```bash
git clone https://github.com/CV17-09/Houston-Flood-Data-Pipeline.git

cd Houston-Flood-Data-Pipeline
```

---

## Create a Virtual Environment

```bash
python -m venv venv
```

### Activate

Mac/Linux

```bash
source venv/bin/activate
```

Windows

```bash
venv\Scripts\activate
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# ⚙ Environment Variables

Create a `.env` file.

```env
WEATHER_API_KEY=your_api_key

DB_HOST=localhost
DB_PORT=5432
DB_NAME=houston_flood_db
DB_USER=postgres
DB_PASSWORD=your_password
```

---

# ▶ Running the Pipeline

Run the complete ETL workflow:

```bash
python scripts/run_pipeline.py
```

Or execute each stage individually:

```bash
python scripts/extract_weather.py

python scripts/transform_weather.py

python scripts/load_to_postgres.py
```

---

# 🔍 Example SQL Queries

## High-Risk Locations

```sql
SELECT
    l.location_name,
    l.zip_code,
    f.risk_score,
    f.risk_level,
    w.rainfall
FROM flood_risk_scores f
JOIN weather_observations w
ON f.observation_id = w.observation_id
JOIN locations l
ON w.location_id = l.location_id
WHERE f.risk_level IN ('High Risk','Severe Risk')
ORDER BY f.risk_score DESC;
```

---

## Average Rainfall

```sql
SELECT
    l.location_name,
    AVG(w.rainfall) AS average_rainfall
FROM weather_observations w
JOIN locations l
ON w.location_id = l.location_id
GROUP BY l.location_name
ORDER BY average_rainfall DESC;
```

---

# 💡 Key Insights

This pipeline enables analysts to:

* Identify neighborhoods with repeated heavy rainfall
* Detect locations experiencing increasing flood risk
* Analyze precipitation trends over time
* Support emergency response planning
* Produce interactive reports for stakeholders

---

# 🚀 Future Enhancements

* Automate scheduled ETL jobs with Apache Airflow
* Integrate NOAA weather feeds
* Incorporate Harris County flood-warning systems
* Add GIS mapping with GeoPandas
* Deploy to Microsoft Azure or AWS
* Implement real-time flood alerts
* Build a Streamlit analytics application
* Develop a React dashboard for public visualization




