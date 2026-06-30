# Houston Flood Data Pipeline

## Overview

Houston Flood Data Pipeline is an end-to-end data engineering project that collects weather data, transforms it with Python, stores structured results in PostgreSQL, and supports a Power BI dashboard for identifying Houston areas with elevated flood risk.

The goal of this project is to demonstrate how real-time or historical weather data can be processed into actionable insights for flood-risk monitoring, emergency planning, and data-driven decision-making.

## Project Timeline

**06/20/2026 – 07/15/2026**

## Problem Statement

Houston is highly vulnerable to flooding due to heavy rainfall, flat terrain, bayous, and rapid urban development. Raw weather data alone is difficult to interpret without transformation, storage, and visualization.

This project solves that problem by building a pipeline that collects weather data, cleans and transforms it, stores it in a relational database, and visualizes flood-risk indicators in Power BI.

## Features

* Pulls weather data from an external weather API
* Cleans and transforms raw weather data using Python
* Stores processed data in PostgreSQL
* Calculates flood-risk indicators based on rainfall and weather conditions
* Supports Power BI dashboards for visualization
* Highlights Houston areas with elevated flood risk
* Provides a repeatable ETL workflow for data updates

## Tech Stack

* **Python** – Data extraction, transformation, and pipeline logic
* **PostgreSQL** – Relational database storage
* **Power BI** – Dashboard and flood-risk visualization
* **Pandas** – Data cleaning and transformation
* **Requests** – API data extraction
* **SQLAlchemy / psycopg2** – PostgreSQL connection
* **Weather API** – Weather and rainfall data source

## Project Architecture

```text
Weather API
   ↓
Python ETL Pipeline
   ↓
Data Cleaning & Transformation
   ↓
PostgreSQL Database
   ↓
Power BI Dashboard
   ↓
Houston Flood Risk Insights
```

## Data Pipeline Workflow

### 1. Extract

The pipeline retrieves weather data for Houston-area locations from a weather API. Data may include:

* Temperature
* Humidity
* Wind speed
* Rainfall
* Precipitation probability
* Weather conditions
* Timestamp
* Location or ZIP code

### 2. Transform

Python is used to clean and prepare the data by:

* Removing missing or invalid values
* Standardizing timestamps
* Formatting location fields
* Converting data types
* Calculating rainfall totals
* Creating flood-risk categories

Example flood-risk labels:

```text
Low Risk
Moderate Risk
High Risk
Severe Risk
```

### 3. Load

The transformed data is loaded into PostgreSQL tables for structured storage and querying.

Example database tables:

```text
locations
weather_observations
flood_risk_scores
pipeline_logs
```

### 4. Visualize

Power BI connects to PostgreSQL and displays:

* Rainfall trends
* Flood-risk scores
* High-risk Houston areas
* Weather condition summaries
* Risk level by location
* Time-based precipitation patterns

## Example Database Schema

```sql
CREATE TABLE locations (
    location_id SERIAL PRIMARY KEY,
    location_name VARCHAR(100),
    zip_code VARCHAR(10),
    latitude DECIMAL,
    longitude DECIMAL
);

CREATE TABLE weather_observations (
    observation_id SERIAL PRIMARY KEY,
    location_id INT REFERENCES locations(location_id),
    observation_time TIMESTAMP,
    temperature DECIMAL,
    humidity DECIMAL,
    wind_speed DECIMAL,
    rainfall DECIMAL,
    precipitation_probability DECIMAL,
    weather_condition VARCHAR(100)
);

CREATE TABLE flood_risk_scores (
    risk_id SERIAL PRIMARY KEY,
    observation_id INT REFERENCES weather_observations(observation_id),
    risk_score DECIMAL,
    risk_level VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Flood Risk Logic

Flood risk is estimated using weather indicators such as rainfall amount, precipitation probability, and humidity.

Example logic:

```text
Rainfall >= 3 inches → Severe Risk
Rainfall >= 2 inches → High Risk
Rainfall >= 1 inch  → Moderate Risk
Rainfall < 1 inch   → Low Risk
```

This logic can be improved by adding bayou levels, drainage data, historical flood records, or geospatial information.

## Power BI Dashboard

The Power BI dashboard includes:

* Flood risk by Houston area
* Rainfall by location
* Daily precipitation trends
* Risk-level summary cards
* High-risk location table
* Weather condition breakdown

The dashboard helps users quickly identify which Houston areas may need closer monitoring during heavy rainfall events.

## Folder Structure

```text
Houston-Flood-Data-Pipeline/
│
├── data/
│   ├── raw/
│   └── processed/
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
├── powerbi/
│   └── houston_flood_dashboard.pbix
│
├── config/
│   └── database_config.py
│
├── requirements.txt
├── README.md
└── .gitignore
```

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/Houston-Flood-Data-Pipeline.git
cd Houston-Flood-Data-Pipeline
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate the virtual environment:

```bash
# Mac/Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the root directory:

```env
WEATHER_API_KEY=your_api_key_here
DB_HOST=localhost
DB_NAME=houston_flood_db
DB_USER=postgres
DB_PASSWORD=your_password
DB_PORT=5432
```

## Running the Pipeline

Run the full pipeline:

```bash
python scripts/run_pipeline.py
```

Or run each step individually:

```bash
python scripts/extract_weather.py
python scripts/transform_weather.py
python scripts/load_to_postgres.py
```

## Sample SQL Queries

Find high-risk areas:

```sql
SELECT 
    l.location_name,
    l.zip_code,
    f.risk_score,
    f.risk_level,
    w.rainfall,
    w.observation_time
FROM flood_risk_scores f
JOIN weather_observations w 
    ON f.observation_id = w.observation_id
JOIN locations l 
    ON w.location_id = l.location_id
WHERE f.risk_level IN ('High Risk', 'Severe Risk')
ORDER BY f.risk_score DESC;
```

Average rainfall by location:

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

## Key Insights

This project can help identify:

* Houston areas with repeated heavy rainfall
* Locations with increasing flood-risk scores
* Time periods with elevated precipitation
* Patterns between weather conditions and flood risk

## Future Improvements

* Add real-time automated scheduling
* Include bayou and river water-level data
* Add geospatial mapping with latitude and longitude
* Integrate Harris County flood warning data
* Deploy the pipeline to the cloud
* Add alerts for severe flood-risk conditions
* Build a web dashboard using Streamlit or React

