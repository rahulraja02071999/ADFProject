End-to-End Azure Data Engineering Pipeline:
--------------------------------------------

Azure Data Factory | Azure Data Lake Gen2 | Medallion Architecture

📌 Project Overview
   -----------------

This project demonstrates an end-to-end data ingestion and transformation pipeline built using Azure Data Factory (ADF) and Azure Data Lake Gen2, following the Medallion Architecture (Bronze → Silver → Gold).

The solution integrates On-Premise files, GitHub data, and SQL databases with support for full and incremental loads, scalable orchestration, and production-ready transformations.

🏗️ Architecture
   -------------
On-Prem Files | GitHub | SQL
        ↓
Azure Data Factory (ADF)
        ↓
Azure Data Lake Gen2
Bronze → Silver → Gold

🥉 Bronze Layer – Raw Data Ingestion
   ----------------------------------
1)On-Premise Data
---------------

-> Integration Runtime hosted on local machine and registered with ADF using authentication key.

-> Ingested multiple on-prem files dynamically using:
	- ForEach activity
	- Parameterized datasets
	- Dynamic column mappings

-> Raw files stored in Bronze container of Azure Data Lake Gen2.

2)GitHub Data
--------------

-> Used Web Activity to fetch data from GitHub URLs.

-> Leveraged Copy Activity to load GitHub data into Bronze layer.

-> Ensured standardized raw storage format in Data Lake.

3️)SQL Data (Full & Incremental Load)
--------------------------------------

-> Implemented timestamp-based incremental loading using watermark logic.

-> Used Lookup Activities to:
	- Fetch last_load_timestamp (default: 1900-01-01)
	- Fetch current_max_timestamp

-> Full load executed during first run.

-> Incremental loads process only new/updated records.

-> Updated watermark stored using a metadata JSON file for future runs.

🔁Parent Pipeline & Orchestration
  -------------------------------- 

-> Created a parent pipeline to orchestrate:
	- On-Prem ingestion
    - GitHub ingestion
	- SQL ingestion

-> Used Execute Pipeline activity with parameter passing.

-> Implemented error handling and monitoring.

-> Integrated Logic Apps for pipeline success/failure alerts.

🥈 Silver Layer – Data Transformation
   -----------------------------------
   
-> Used ADF Mapping Data Flows for data transformation.

-> Key transformations applied:
	- Select & Rename columns
	- Derived columns (Regex, Uppercase, Casting)
	- Filters & Data cleansing
	- Alter Row logic

-> Stored transformed data in Delta format for optimized analytics.

🥇 Gold Layer – Business-Ready Data
    --------------------------------

-> Built aggregated datasets and business views from Silver layer.

-> Applied transformations like:
	- Aggregations
	- Top-N analysis

-> Designed for reporting, analytics, and downstream consumption.

🛠️ Technologies Used
   ------------------
-> Azure Data Factory (ADF)

-> Azure Data Lake Gen2

-> Self-Hosted Integration Runtime

-> Mapping Data Flows

-> Delta Lake

-> Azure Logic Apps

-> SQL

-> GitHub (Web ingestion)

🚀 Key Highlights
   ---------------
   
-> Dynamic and reusable ADF pipelines

-> Full & incremental data loading

-> Medallion architecture implementation

-> Scalable orchestration with parent-child pipelines

-> Production-style monitoring and alerting

-> Optimized storage using Delta format

📈 Learning Outcome
   -----------------
   
-> This project enhanced my practical understanding of:

-> Azure Data Engineering best practices

-> Data pipeline orchestration

-> Incremental loading strategies

-> Cloud-based data lake design

-------------------------------------------------------------------------------------

⭐ If you find this project useful, feel free to star the repository!

-------------------------------------------------------------------------------------
