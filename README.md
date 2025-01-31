# Azure NYC-Taxi data

## Introduction
This project serves as a comprehensive implementation to building an end-to-end data engineering pipeline. It covers each stage from data ingestion to processing and finally to storage, utilizing Azure Cloud Services and Databricks Lakehouse Architecture as a core.

## System Architecture
![System Architecture](https://github.com/maihuy-dataguy/Azure-NYC-Taxi-project/blob/main/pics/flow.png)

The project is designed with the following components:

- **Data Source**: We use 2 files taxi_zone_lookup.csv and trip_type.csv alongside with NYC-Taxi trip data API from `https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page` for our pipeline.
- **Azure Data Factory (ADF)**: Responsible for ingesting data and storing fetched data in azure data lakehouse at bronze layer, implenmenting parameterized pipeline to fully fetch 12-months data in 2023.
- **Databricks Lakehouse**: Using medallion architecture, we transfer our data between these layers including bronze, silver, gold layers
    - Bronze layer: Used for storing raw data ingested from ADF.
    - Silver layer: Used for storing transformed data (parquet format) through spark using databrick notebook.
    - Gold layer: Used for storing transformed (delta format), creating delta tables on top of data, thanks to transactional log created from delta lake, using sql (sparkSQL) to query data for  auditing, reports in combination with data versioning and time travel to enhance ACID features and data integrity in azure data lake.
- **Power BI**: For creating dashboards to support related reports. 
- **Securiy**: Using secret key, grant access service princle application as storage data contributor.

## Technology Stack
- **Azure Data Factory (ADF)**: For orchestrating data movement and transformation.
- **Azure Data Lake Storage (ADLS)**: For storing raw and processed data.
- **Azure Databricks**: For data transformation and processing.
- **Delta Lake** : For table format that extends Parquet data files with a file-based transaction log for ACID transactions and scalable metadata handling.
- **Power BI**: For data visualization and reporting.
- **Azure Key Vault**: For securely managing credentials and secrets.

