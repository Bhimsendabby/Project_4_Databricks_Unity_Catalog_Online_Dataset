# Multi-Year Data Analytics & Transformation (Databricks & Unity Catalog)

## 📌 Project Overview
This project demonstrates an end-to-end cloud data engineering solution using Azure Databricks and Unity Catalog, orchestrated by Azure Data Factory. The goal is to ingest multi-year (2019–2021) raw datasets from external GitHub repositories, apply a Medallion Architecture (Bronze, Silver, Gold), and perform advanced data transformations and visualizations.

By utilizing Unity Catalog, we ensure robust data governance through structured Catalogs, Schemas, and Volumes, while Databricks Notebooks handle complex data processing and aggregation using PySpark and Plotly.

## 🏗️ Architecture Diagram
The pipeline follows a modern cloud data architecture:
![project_4](https://github.com/user-attachments/assets/617134b8-2a04-4f5e-ac5c-05da70749ec6)


1. **Source:** Raw CSV files (2019, 2020, 2021) fetched via HTTP from GitHub.

2. **Ingestion & Storage:** Unity Catalog setup involving the creation of a dedicated Catalog, Schema, and Volume for raw file storage.

3. **Bronze:** Raw landing of files into Unity Catalog Volumes.
   
4. **Silver:** Data cleaning, renaming columns for suitability, and schema enforcement.

5. **Gold:** Final aggregated datasets ready for business reporting.
   
6. **Orchestration:** Azure Data Factory (ADF) pipelines to automate and schedule notebook execution.
 
7. **Visualization:** Data insights generated using Plotly and Matplotlib within Databricks.

8. **Metadata Management:** (Optional) Implementation of a dynamic metadata-driven loading process for the Silver layer.

## Repository Structure

```text
├── Code/
│   ├── BronzeToSilver/                # Logic to create Catalog, Schema, and Volumes
│   └── SilverToGold/                  # Silver/Gold transformations & Aggregations and Generating visuals with Plotly/Matplotlib
├── Screenshots/
│   ├── Architecture Diagram/          # Diagram for Architecture
└── README.md                          # Project documentation
```



## Pipeline Workflow
**Step 1:** Governance Setup & Ingestion
We begin by establishing a secure environment in Unity Catalog. A new Catalog and Schema are defined, and a Volume is created to serve as the landing zone. A Databricks notebook programmatically fetches three years of data (2019–2021) from GitHub and writes them into this volume with standardized column naming conventions.


**Step 2:** Medallion Transformation
Data is moved from the Volume into Delta Tables:

Cleaning: Removing nulls and formatting data types.

Aggregation: Creating summary tables based on specific column dimensions to derive business value.

Metadata (Optional): A Delta-based metadata table tracks the state of the pipeline, allowing for dynamic loading into the Silver layer.

**Step 3:** Orchestration with ADF
To automate the workflow, an Azure Data Factory pipeline is configured:

Linked Services connect ADF to the Databricks Workspace.

The Notebook Activity triggers the transformation logic.

Triggers/Schedules are applied to ensure data remains current without manual intervention.

**Step 4:** The final Gold layer is analyzed visually. By integrating the Plotly package (via matplotlib bridge or direct import), we generate interactive charts to identify trends across the 2019–2021 period.


📊 Business Insights
 - Temporal Trends: Comparative analysis of metrics across 2019, 2020, and 2021.
 - Governance & Security: Centralized access control and data lineage via Unity Catalog.
 - Scalability: The metadata-driven approach allows for adding new years of data by simply updating a configuration table.

## 👤 Author and Contributors
Bhim Sen

