# Fintech Data Migration Pipeline

This repository showcases scalable data pipeline designed for migrating and transforming a fintech company’s data from traditional SQL databases to Azure Data Lake. It employs a medallion architecture within ADLS Gen2 using PySpark and Delta Lake for efficient data management and processing. The project also features automated email notifications for tracking pipeline success or failure, enhancing operational visibility and responsiveness.

---
## Video Documentation
Link: [YouTube](https://youtu.be/adW2WUgc55s)

## **Pipeline Overview**

The pipeline performs the following key tasks:

1. **Data Ingestion**:
   - Uses a **Lookup Activity** to fetch metadata (`schema_name`, `table_name`) from an Azure SQL Database.
   - A **ForEach Activity** runs the **Copy Activity**, transferring data from the SQL database to the `bronze` file system in ADLS Gen2.

2. **Data Transformation**:
   - **BronzeToSilverNotebook**: Cleans and transforms raw data from the bronze layer into structured, enriched data in the silver layer using **Azure Synapse Analytics**. The transformed data is then stored in a new `silver` file system in ADLS Gen2.
   - **SilverToGoldNotebook**: Further transforms the data and creates optimized analytical tables in the `gold` file system, making the data ready for analytics and reporting.

3. **Notifications**:
   - Utilizes **Azure Logic Apps** to send email notifications on pipeline success or failure.

---

## **Tech Stack**

- **Azure Synapse Analytics**: Orchestration and data transformation through notebooks.
- **Delta Lake**: Schema evolution and ACID-compliant storage for data.
- **Azure Data Lake Storage (ADLS Gen2)**: Storage for bronze, silver, and gold data layers.
- **Azure SQL Database**: Source of data for migration.
- **Azure Logic Apps**: Automated notifications for pipeline status.

---

## **Pipeline Workflow**
![Pipeline Workflow](https://github.com/tahir007malik/fintechDataMigration/blob/main/docs/fintechDataMigration-worflow.png)

1. **Data Ingestion**:
   - Fetch `schema_name` and `table_name` using **Lookup Activity** from the Azure SQL database.
   - Use **ForEach Activity** to iterate over each table and copy the data to the `bronze` file system in ADLS Gen2.

2. **Data Transformation**:
   - **BronzeToSilverNotebook**: This notebook performs cleaning and transformation operations to turn the raw data into structured formats. The transformed data is saved in the `silver` file system in ADLS Gen2.
   - **SilverToGoldNotebook**: This notebook further optimizes the data for analytical purposes, creating the gold layer and storing it in the `gold` file system.

3. **Notifications**:
   - A **Logic App Trigger** is set up to send success or failure email notifications based on the status of the pipeline.

---

## **Getting Started**

### **Prerequisites**
- An **Azure Subscription** with access to **Azure Synapse Analytics**, **ADLS Gen2**, **Azure SQL Database**, and **Azure Logic Apps**.

### **Setup Instructions**
1. **Configure Azure Synapse Analytics**:
   - Set up the **Lookup Activity** to fetch `schema_name` and `table_name` from the Azure SQL Database.
   - Configure the **ForEach Activity** with the **Copy Activity** to migrate data to the `bronze` file system in ADLS Gen2.

2. **Create Notebooks in Azure Synapse Analytics**:
   - Implement the **BronzeToSilverNotebook** to clean and transform the data, storing the output in the `silver` file system.
   - Implement the **SilverToGoldNotebook** to optimize the data for analytical processing, storing the output in the `gold` file system.

3. **Configure Logic Apps**:
   - Create an automated workflow to send success or failure email notifications based on the pipeline status.

---

## **Run the Pipeline**

Once all configurations are complete, trigger the pipeline in **Azure Synapse Analytics**. The pipeline will:

- Fetch schema and table names from Azure SQL.
- Copy data to the `bronze` file system in ADLS Gen2.
- Transform data through the notebooks (bronze -> silver -> gold), saving results to the respective file systems (`silver`, `gold`).
- Send email notifications upon completion or failure.

---

## **Notifications**

- **Success Notification**: Sent when the pipeline runs successfully from ingestion to transformation.
- **Failure Notification**: Sent if any part of the pipeline fails.

---
