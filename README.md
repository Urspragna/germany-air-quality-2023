# Germany Air Quality Analysis 2023

**M.Sc. Big Data**

Distributed analysis of PM10 and PM2.5 particulate matter across Germany in 2023, using Apache Spark on a 4-node HDFS cluster. Covers the full pipeline from raw sensor ingestion to interactive dashboards and a 30-day forecast.

## Notebooks

| File | Description |
|---|---|
| `air_quality_analysis.ipynb` | Main analysis — ETL, interactive Plotly dashboards, outlier detection, spatial hotspots, correlation heatmap, Prophet forecast |
| `time_series_forecast.ipynb` | Dedicated time-series analysis and forecasting |

## What's inside

- **Data ingestion** — PySpark reads 2.8M+ SDS011 sensor readings from HDFS (`DE_2023-*_sds011.csv`)
- **Cleaning** — value range filtering, null removal, coordinate bounds
- **Interactive dashboards** — Plotly: daily trend with 7/30-day rolling averages, seasonal patterns (hour / weekday / month), WHO limit lines
- **Outlier detection** — IQR fences + z-score flagging, Winsorisation
- **Air-quality calendar** — colour-coded heatmap (Good / Moderate / Sensitive / Unhealthy) by day
- **Spatial hotspot map** — scatter plot of mean PM2.5 per sensor location, top-15 risk ranking
- **Correlation heatmap** — Pearson r between PM10, PM2.5, hour, and month
- **30-day PM2.5 forecast** — Facebook Prophet (yearly + weekly seasonality, 90% CI); fallback to 30-day MA
- **Action dashboard** — KPI indicators for worst month, worst hour, worst day, trend direction

## Tech stack

`PySpark` · `HDFS` · `Plotly` · `Prophet` · `Pandas` · `NumPy` · `Python 3`

## Key findings

- PM2.5 trend is slightly **worsening** over 2023
- Worst month: **January** (winter heating)
- Worst hour: **morning rush hour**
- ~78% of sensor locations exceed the WHO annual PM2.5 guideline of 15 µg/m³

## How to run

The notebooks use `%pyspark` magic and require a running Spark cluster with HDFS.  
To explore the analysis logic locally, replace the Spark read cell with a pandas CSV read.
