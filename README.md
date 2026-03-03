# Intel IoT Data Analytics

## Overview

This project performs advanced data analytics on large-scale IoT sensor datasets from agricultural operations. The system implements a comprehensive ETL pipeline (Extract, Transform, Load) with multi-stage data processing to extract actionable insights for farm management.

## Project Objectives

- Ingest and process high-volume IoT sensor data from distributed farming operations
- Implement a scalable, multi-tier data architecture (Bronze → Silver → Gold layers)
- Identify and remediate data quality issues through anomaly detection
- Generate aggregated analytics and business intelligence visualizations

## Workflow

### 1. Data Generation

Generate or scale the raw IoT sensor dataset using the provided scripts.

### 2. Bronze ETL (Raw Data Ingestion)

- Load raw CSV data from IoT sensors
- Add ingestion timestamp metadata
- Store as Parquet format for efficient processing

### 3. Technical EDA (Exploratory Data Analysis)

- Analyze Bronze layer data
- Identify anomalies and data quality issues (e.g., out-of-bounds metrics, missing values)
- Document findings in Jupyter notebooks

### 4. Silver ETL (Data Cleaning)

- Filter and remove identified anomalies
- Validate and standardize data formats
- Persist cleaned data as Parquet files

### 5. Gold ETL (Data Aggregation)

- Aggregate Silver layer data by `farm_id`, `cow_id`, and hourly intervals
- Apply statistical transformations (mean, max, sum)
- Export aggregated results as Parquet or CSV

### 6. Business EDA & Dashboarding

- Build interactive visualizations using Plotly or Streamlit
- Create farmer-friendly dashboards from Gold layer data
- Enable real-time monitoring and decision support

## Technology Stack

- **Data Processing**: Python, Pandas, PySpark
- **Storage**: Parquet, CSV
- **Visualization**: Plotly, Streamlit
- **Notebooks**: Jupyter

## Project Structure

```
intel-iot-data-analytics/
├── data/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── notebooks/
├── src/
│   ├── etl/
│   └── dashboards/
└── README.md
```

## Project Phases

### Phase#1 Getting Started

#### Create folder structure

mkdir -p data/bronze data/silver data/gold scripts notebooks

#### Create the LOCAL Conda Environment needed for the ETL pipeline

conda create --prefix ./env python=3.10 pandas numpy matplotlib scikit-learn polars pyarrow jupyter pyarrow fastparquet tqdm -y

#### Activate the local environment

conda activate ./env
jupyter notebook

### Phase#2 Data Generation (The "Raw" Data)

Since real 2,000-cow datasets are under corporate NDA, we wrote a Python script to generate a highly realistic "Digital Twin" dataset. It simulates diurnal temperature, heat stress affecting rumination, and hardware failures (dead batteries).

- step#1: Download the sensor_data from Kaggle
  -- way#1
  link: https://www.kaggle.com/datasets/hienvuvg/mmcows?resource=download-directory&select=sensor_data

  -- way#2

  ```
  pip install kaggle
  kaggle datasets download -d hienvuvg/mmcows -p ./data --unzip
  ```

NOTE: We mainly focus on structured data provided by "sensor_data" in the main dataset.

#### Main Data Focus:

- main_data/immu: The core accelerometer firehose (The behavior physics).

- behavior_labels/individual: The ground truth (Eating, Resting, Rumination).

- main_data/thi (or weather): Temperature Humidity Index (The environmental stressor).

- sub_data/health_records (or cbt): The actual welfare outcomes.

## License

MIT
