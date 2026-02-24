# Customer Account Analysis & Data Warehousing (Azure Synapse)

## 📌 Project Overview
This project demonstrates an end-to-end Data Warehousing solution built on Azure Synapse Analytics. The goal is to provide a financial institution with a scalable architecture to consolidate customer transaction data, perform complex transformations, and deliver actionable insights through Power BI.

By leveraging the Medallion Architecture, we transition raw CSV data into a high-performance Delta Lake format and a Dedicated SQL Pool, ensuring data integrity with SCD Type 1 logic and optimized distribution strategies.

## 🏗️ Architecture Diagram
The pipeline follows a modern cloud data architecture:
![onprem_to_adl_to_synapse_to_powerbi (2)](https://github.com/user-attachments/assets/ba95fc66-60fe-41ef-8f5d-22851cfdb938)

The pipeline follows a modern cloud data warehouse architecture:

Source: 

Ingestion & ETL: 

Storage: 

Serverless Layer: 

Warehouse Layer: Dedicated SQL Pool for high-performance relational storage using Hash, Round-Robin, and Replicated distributions.

Visualization: Power BI for customer insights.

1. **Source:** Raw transaction data in CSV format uploaded to ADLS Gen2.

2. **Ingestion & ETL:** Synapse Dataflows for Delta conversion and SCD Type 1 logic in Delta Format.

3. **Storage:** Azure Data Lake Storage Gen2 (Bronze/Silver/Gold layers).

4. **Serverless Layer:** Synapse Serverless SQL Pools for ad-hoc querying and Power BI views.

5. **Warehouse Layer:**  Dedicated SQL Pool for high-performance relational storage using Hash, Round-Robin, and Replicated distributions.

6. **Layers:** Bronze (Raw), Silver (Cleaned), and Gold (Business-ready).

7. **Schema Management:** SCD Type 1 for dimensional integrity.

## Repository Structure

```text
├── Code/
│   ├── BronzeToSilver/                # Dataflows for converting raw CSV to Delta format
│   └── SilverToGold/                  # Dataflow logic for Dimension table updates
├── Screenshots/
│   ├── Architecture Diagram/          # Diagram for Architecture
│   └── Dedicated_Pool/                # DDL for Hash, Round-Robin, and Replicated tables
└── README.md                          # Project documentation
```



## Pipeline Workflow
**Step 1:** Data Ingestion & Delta Conversion
Raw financial data is ingested from ADLS Gen2 in CSV format. Using Synapse Dataflows, the data is transformed into Delta format to enable ACID transactions and time-travel capabilities within the Data Lake.


**Step 2:** SCD Type 1 Implementation
To maintain the "Current State" of customer accounts:

Implemented SCD Type 1 using Synapse Dataflows to overwrite existing records with updated information.

The output is stored as a Delta Table in ADLS Gen2.

The data is exposed via Serverless SQL Pools for immediate querying without needing to load a warehouse.

**Step 3:** Serverless SQL & Power BI Integration
To minimize costs while maintaining performance:

Created SQL Views in the Serverless pool pointing to the Gold-layer Delta files.

Connected Power BI directly to these views to provide real-time customer insights.

**Step 4:** Dedicated SQL Pool Optimization
For heavy analytical workloads, a Dedicated SQL Pool was designed with specific distribution strategies.
<img width="689" height="148" alt="image" src="https://github.com/user-attachments/assets/45c39a9a-b64d-43f3-aa9d-6ca4f532bc73" />

Note: We established PK/FK relationships and Clustered Columnstore Indexes for maximum query performance.

📊 Business Insights
 - Customer Segmentation: Analysis of transaction volumes per account type.
 - Data Integrity: Reliable "Single Version of Truth" maintained via SCD Type 1.
 - Performance: Sub-second query response times using Distributed SQL Pool architectures.
   
## 👤 Author and Contributors
Bhim Sen

