# US Electricity Analytics Platform

An end-to-end data engineering and analytics project built using **Azure Databricks, PySpark, SQL, ADLS Gen2 and Power BI**. The platform processes hourly US electricity data from the U.S. Energy Information Administration (EIA) to analyse demand, generation, imports, exports and electricity demand forecast accuracy.

## Project Overview

The project analyses electricity consumption and generation across selected US grid operators. It focuses on understanding:

- Peak electricity demand across grid operators.
- Generation contribution by fuel type during peak demand.
- Electricity imports and exports.
- Actual demand versus day-ahead demand forecasts.
- Forecast accuracy across grid operators.

## Architecture

**Data Source:** U.S. Energy Information Administration (EIA) API

**Data Flow:**

EIA API → ADLS Gen2 (Raw) → Bronze → Silver → Gold → Power BI

The project follows the Medallion Architecture.

| Layer | Implementation |
|---|---|
| Raw | Original EIA API responses stored in ADLS Gen2 |
| Bronze | Auto Loader-based ingestion into Delta tables |
| Silver | Data transformation, deduplication and historical tracking using AUTO CDC |
| Gold | Analytical materialized views for reporting |

## Technology Stack

- **Cloud:** Microsoft Azure
- **Data Engineering:** Azure Databricks, PySpark, Spark SQL
- **Storage:** Azure Data Lake Storage Gen2
- **Data Processing:** Delta Lake, Auto Loader, AUTO CDC
- **Governance:** Unity Catalog
- **Secrets Management:** Azure Key Vault
- **Reporting:** Power BI
- **Source:** EIA API

## Power BI Dashboard

The dashboard provides an overview of electricity demand, generation and forecast performance.

Key insights include:

- Highest observed peak demand by grid operator.
- Actual versus forecast demand at peak hours.
- Generation mix by fuel type.
- Demand, net generation and interchange comparisons.
- Forecast accuracy metrics.

The dashboard is available in the [`powerbi`](powerbi/) directory.

## Data Scope and Limitations

- Data is sourced from the EIA API.
- The current implementation covers five balancing authorities: AVA, BPAT, CISO, PGE and SCL.
- Peak demand values represent the highest observations within the available dataset, not necessarily complete annual peaks.
- Generation and interchange data can arrive later than demand and forecast data.
- Some source-level energy balance discrepancies remain under investigation.

## Project Status

The initial end-to-end implementation and Power BI MVP are complete. The project is currently undergoing data validation and testing.

## Future Enhancements

- Expand coverage to additional grid operators.
- Improve monitoring of data arrival delays and pipeline health.
- Extend historical analysis as more data becomes available.
- Add data quality and pipeline monitoring dashboards.
