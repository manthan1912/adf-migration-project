# Azure Data Factory: On-Prem SQL Server to Azure Blob Delimited Text

This project contains an Azure Data Factory (ADF) pipeline that copies data from an **on-premises SQL Server** database to **Azure Blob Storage** as a **delimited text file**.

## Project Overview

The solution uses Azure Data Factory to extract data from an on-prem SQL Server table and write it to Azure Blob Storage through a **Self-hosted Integration Runtime (SHIR)**.

### Main purpose
- Read data from an on-prem SQL Server table
- Transfer it securely through SHIR
- Store the output in Azure Blob Storage
- Save the output as a **delimited text file**

## Pipeline Details

### Pipeline
- **Name:** `COPY-ONPREM-TABLE-BLOB-PARQUET`

### Activity
- **Name:** `COPY-ONPREM-TABLE-TO-BLOB-PARQUET`


## Source Configuration

The source is an on-prem SQL Server table.

### Linked Service
- **Name:** `LS_ONPREM_SQL_TO_BLOB_PARQ`
- **Type:** SQL Server
- **Authentication:** SQL Authentication

### Source Database
- **Server:** `LAPTOP-XXXXX`
- **Database:** `AdventureWorksLT2025`

### Source Dataset
- **Dataset name:** `SqlServerTable1`
- **Schema:** `SalesLT`
- **Table:** `Customer`

## Sink Configuration

The sink is Azure Blob Storage.

### Linked Service
- **Name:** `LS_FOR_AZ_BLOB_EXCEL`
- **Type:** Azure Blob Storage

### Output Dataset
- **Dataset name:** `onprem_to_azure_excel_test`
- **Format:** Delimited Text
- **Container:** `output`
- **Column delimiter:** `,`
- **First row as header:** `true`
- **Quote character:** `"`
- **Escape character:** `\`

### Sink Behavior
The pipeline currently writes output using:
- **Sink type:** `DelimitedTextSink`
- **File extension:** `.txt`

## Integration Runtime

This project uses a **Self-hosted Integration Runtime** to connect Azure Data Factory to the on-prem SQL Server environment.

### Integration Runtime
- **Name:** `onprem-sqlserver-IR`
- **Type:** Self-hosted

## Files in This Project

This repository may include exported ARM templates such as:

- `ARMTemplateForFactory.json`
- `ARMTemplateParametersForFactory.json`
- `adf-for-basicprojects_ARMTemplateForFactory.json`
- `adf-for-basicprojects_ARMTemplateParametersForFactory.json`
- `ArmTemplate_0.json`
- `ArmTemplate_master.json`
- `ArmTemplateParameters_master.json`

These files are used to deploy or version the ADF resources.

## Deployment Requirements

Before deploying or running this project, make sure you have:

- An Azure Data Factory instance
- An Azure Blob Storage account
- A Blob container named `output` or an updated container configuration
- Access to the on-prem SQL Server instance
- A working Self-hosted Integration Runtime installed and registered
- Valid credentials for:
  - SQL Server
  - Azure Blob Storage

## How It Works

1. Azure Data Factory connects to the on-prem SQL Server through the Self-hosted Integration Runtime.
2. The pipeline reads data from the `SalesLT.Customer` table.
3. The copy activity transfers the data to Azure Blob Storage.
4. The output is stored as a **delimited text file** in the configured blob container.

