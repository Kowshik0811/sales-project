🛠️ Sales Data Pipeline Project
This project demonstrates a cloud-native data ingestion and transformation pipeline for sales data using Azure Data Factory (ADF). It reads raw sales-related files from a public GitHub repository, processes them through ADF pipelines, and stores the output in Azure Data Lake Storage Gen2.

📂 Project Structure
The pipeline processes five key entities:

Customer

Date

Market

Product

Transaction

These files are fetched from a GitHub repository in CSV format, processed via ADF, and landed in structured folders in the data lake.

⚙️ Technologies Used
Azure Data Factory (ADF)

Azure Data Lake Storage Gen2

GitHub (as external HTTP source)

JSON-based Parameterization

ADF Datasets, Linked Services, and Pipelines

📁 Data Flow Overview
Source: Public GitHub repository (raw.githubusercontent.com)

Ingestion: HTTP Linked Service fetches data using ADF pipelines.

Parameterization: A JSON parameter file (git.json) in the Data Lake controls dynamic file names and paths.

Storage: Data is stored in Azure Data Lake in appropriate folders (partitioned by entity/date if applicable).

Sink Structure (example):

bash
Copy
Edit
/sales-data/
  ├── customer/
  ├── date/
  ├── market/
  ├── product/
  └── transaction/
🔗 Linked Services
AzureDataLakeStorage: Connected to https://salesproject0811.dfs.core.windows.net/

gittoazure: Public HTTP connection to GitHub raw content

🧾 Parameter File (git.json)
A JSON schema stored in the parameters file system in Azure Data Lake. Controls:

p_rel_url: Relative URL of source file

p_sink_folder: Target folder in the lake

p_sink_filename: Output filename

p_relative_urls: Optional for batch loading

🛠️ Pipeline Features
Dynamic file loading using parameterized datasets

Modular architecture for each entity type

Scalable to handle additional entities or schema changes

No authentication required for GitHub access

📌 How to Use
Clone or fork the pipeline definitions into your ADF instance.

Configure the linked services:

Azure Data Lake Storage (set credentials)

GitHub HTTP server (remains anonymous)

Upload git.json with appropriate parameters to parameters/git.json

Trigger the pipeline manually or via schedule

✅ Sample Use Case
Load customer.csv from GitHub and store it in /customer/customer.csv inside Azure Data Lake.

Source:
https://raw.githubusercontent.com/<username>/<repo>/main/data/customer.csv

Sink:
abfss://salesproject0811.dfs.core.windows.net/customer/customer.csv

🚀 Future Enhancements
Add validation checks and logging

Transform raw CSV to Parquet

Build an Azure Synapse or Power BI layer on top

Auto-discovery of new files
