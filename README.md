# End-to-End-Apple-Data-Analysis-Pipeline

This repository showcases an end-to-end Big Data Engineering project that demonstrates the creation of a robust and scalable data pipeline for analyzing Apple-related customer transaction data using Apache Spark and Databricks. 

The project covers the entire ETL (Extract, Transform, Load) process, incorporating modern big data technologies such as Delta Lake for efficient storage and columnar formats like Parquet for optimal performance. By leveraging the PySpark API, this pipeline focuses on tracking customer purchases, particularly those who bought AirPods after iPhone and those who bought only iPhone and AirPods. The project is designed to be easily configurable, scalable, and ready for production-level use.

## 🛠️ Project Structure
-  apple_analysis: Main ETL workflow that coordinates extraction, transformation, and loading operations.
-  reader_factory: A factory pattern to read data from CSV, Parquet, and Delta sources.
-  extractor: Contains classes for extracting data from the sources.
-  transform: Business logic that applies transformations to the extracted data.
-  loader: Handles the process of loading the transformed data into storage.
-  loader_factory: A factory pattern to handle different types of loading mechanisms (e.g., DBFS, Delta).


## 🚀 How to Use the Project
### 1. Clone the Repository:

```bash
   git clone https://github.com/Vikneshwar-GK/End-to-End-Apple-Data-Analysis-Pipeline.git
   cd End-to-End-Apple-Data-Analysis-Pipeline
```
### 2. Set Up the Environment:<br/>

   This project requires Databricks to run. If you don’t have a Databricks account, you can sign up for free on Databricks. Once you have Databricks set up:
   -  Create a Databricks cluster (make sure to use a cluster with PySpark support).
   -  Upload the Python files (apple_analysis.py, reader_factory.py, extractor.py, transform.py, loader.py, loader_factory.py) to Databricks workspace.
   -  Upload the required datasets (Transaction_Updated.csv, Customer_Updated.csv, Products_Updated.csv) to DBFS (Databricks File System). You can do this via the Databricks UI or using Databricks CLI.<br/>
  
   Example paths for DBFS:
   -  Transaction_Updated.csv: /FileStore/tables/Transaction_Updated.csv
   -  Customer_Updated.csv: /FileStore/tables/Customer_Updated.csv
   -  Products_Updated.csv: /FileStore/tables/Products_Updated.csv

### 3. Understand the Code Structure: <br/>

-  Reader Factory (reader_factory.py)
    -  The DataSource abstract class defines how data is read.
    -  The CSVDataSource, ParquetDataSource, and DeltaDataSource classes implement the logic for reading data in respective formats.

-  Extractor (extractor.py)
    -  The AirpodsAfterIphoneExtractor class extracts transactional data from CSV and customer data from Delta.
    -  This data is returned as a dictionary of DataFrames for further processing.

-  Transformer (transform.py)
    -  AirpodsAfterIphoneTransformer: Filters customers who bought AirPods after iPhone.
    -  OnlyAirpodsAndIphoneTransformer: Filters customers who bought only iPhone and AirPods.

-  Loader (loader.py)
    -  The AirPodsAfterIphoneLoader and OnlyAirpodsAndIphoneLoader classes handle the saving of transformed data to DBFS and Delta tables.

-  Loader Factory (loader_factory.py)
    -  A factory to select the appropriate loading mechanism (DBFS, Delta, etc.) based on the requirements.

  
## 🧑‍💻 Running the ETL Pipeline

### 1.  Define Your Workflow<br/>

The project provides two ETL workflows that you can choose to run:
-  First Workflow: Extracts data, transforms it to find customers who bought AirPods after iPhone, and loads the results into DBFS.
-  Second Workflow: Extracts data, transforms it to find customers who bought only iPhone and AirPods, and loads the results into both DBFS and Delta tables.

Example:

If you want to run the First Workflow, you would use the following:

``` python
FirstWorkFlow().runner()
```

For the Second Workflow, use:

``` python
SecondWorkFlow().runner()
```
These workflows are defined in apple_analysis.py.


### 2.  Running on Databricks <br/>

-  In Databricks, open a notebook and import the necessary Python files:
  
``` python
%run "./reader_factory"
%run "./extractor"
%run "./transform"
%run "./loader"
%run "./loader_factory"
%run "./apple_analysis"
```

-  Run the chosen workflow by calling either the FirstWorkFlow().runner() or SecondWorkFlow().runner() depending on which analysis you want to run.


## 🧪 Example Results

### First Workflow: Customers who bought AirPods after iPhone

-  Extract data from Transaction_Updated.csv and Customer_Updated.csv.
-  Transform data to identify customers who bought AirPods after iPhone.
-  Load the result to DBFS in the specified path.

Example Output (DBFS path):

``` python
/FileStore/tables/apple_analysis/output/airpodsAfterIphone
```

### Second Workflow: Customers who bought only iPhone and AirPods

-  Extract data from Transaction_Updated.csv and Customer_Updated.csv.
-  Transform data to find customers who bought only iPhone and AirPods.
-  Load the result to DBFS and Delta tables.

Example Output (DBFS path):

``` python
/FileStore/tables/apple_analysis/output/airpodsOnlyIphone
```
