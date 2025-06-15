# QlikSense_Initial_and_Incremetal_Data_Load_Process-ETL


This repository contains Qlik Sense load script logic to manage full and incremental loading of product inventory data from an Access database into QVD files. It also maintains a simple log mechanism to track task execution.

## 📁 Script Structure

The main components are organized as Qlik Sense subroutines:

### ✅ `CheckLogFile`
- Checks whether the `LogFile.qvd` exists.
- If not, it creates a new log file to track ETL runs.

### 📦 `InitialLoad`
- Performs a full load from the Access database if no previous log entry for the task exists.
- Stores data in `ProductInventory.qvd`.
- Logs the task metadata (start/end time, row count, etc.).

### 🔄 `IncrementalLoad`
- Loads only new records based on the `StockOutDate` field.
- Merges new and existing data into `ProductInventory.qvd`.
- Appends a new entry to the log file for traceability.

## 🔧 Requirements
- Qlik Sense (Desktop or Enterprise)
- Data source: Access DB (`StockManagement_Incremental.accdb`)
- Data connection: `ProductInventory`
- Folder connection: `lib://my_data/`

## 🚀 Execution Order

```qlik
call CheckLogFile;
call InitialLoad;
call IncrementalLoad;
