# Azure Machine Learning Data Prep SDK

You will find in this repo:
- [How-To Guide Notebooks](how-to-guides) for more in-depth feature examples.
- [Case Study Notebooks](case-studies/new-york-taxi) that show in-depth scenario examples of features.
- [Getting Started Tutorial](tutorials/getting-started/getting-started.ipynb) for a quick introduction to the Data Prep SDK and some of its main features.

## Installation
Here are the [SDK installation steps](https://docs.microsoft.com/python/api/overview/azure/dataprep/intro?view=azure-dataprep-py#install).

## Documentation 
Here is more information on how to use the new Data Prep SDK:
- [SDK overview and API reference docs](http://aka.ms/data-prep-sdk) that show different classes, methods, and function parameters for the SDK.
- [Tutorial: Prep NYC taxi data](https://docs.microsoft.com/azure/machine-learning/service/tutorial-data-prep) for regression modeling and then run automated machine learning to build the model.
- [How to load data](https://docs.microsoft.com/azure/machine-learning/service/how-to-load-data) is an overview guide on how to load data using the Data Prep SDK.
- [How to transform data](https://docs.microsoft.com/azure/machine-learning/service/how-to-transform-data) is an overview guide on how to transform data. 
- [How to write data](https://docs.microsoft.com/azure/machine-learning/service/how-to-write-data) is an overview guide on how to write data to different storage locations. 

## Known Issues

- **If running version 0.1.0**: To fix "Error Message: Cannot run the event loop while another loop is running", downgrade Tornado version to 4.5.3. Restart any running kernels for the change to take effect.
```    
pip install -U tornado==4.5.3
```

## Release Notes

### 2019-01-28 (version 1.0.8)

Bug fixes
- Significantly improved the performance of getting data profiles.
- Fixed minor bugs related to error reporting.

### 2019-01-14 (version 1.0.7)

New features
- Datastore improvements (documented in [Datastore how-to-guide](https://github.com/Microsoft/AMLDataPrepDocs/tree/master/how-to-guides/datastore.ipynb))
  - Added ability to read from and write to Azure File Share and ADLS Datastores in scale-up.
  - When using Datastores, Data Prep now supports using service principal authentication instead of interactive authentication.
  - Added support for wasb and wasbs urls.

### 2019-01-09 (version 1.0.6)

Bug fixes
- Fixed bug with reading from public readable Azure Blob containers on Spark.

### 2018-12-19 (version 1.0.4)

New features
- `to_bool` function now allows mismatched values to be converted to Error values. This is the new default mismatch behavior for `to_bool` and `set_column_types`, whereas the previous default behavior was to convert mismatched values to False.
- When calling `to_pandas_dataframe`, there is a new option to interpret null/missing values in numeric columns as NaN.
- Added ability to check the return type of some expressions to ensure type consistency and fail early.
- You can now call `parse_json` to parse values in a column as JSON objects and expand them into multiple columns.

Bug fixes
- Fixed a bug that crashed `set_column_types` in Python 3.5.2.
- Fixed a bug that crashed when connecting to Datastore using an AML image.

### 2018-12-07 (version 0.5.3)

Fixed missing dependency issue for .NET Core2 on Ubuntu 16.

### 2018-12-03 (version 0.5.2)

Breaking changes
- `SummaryFunction.N` was renamed to `SummaryFunction.Count`.
  
Bug fixes
- Use latest AML Run Token when reading from and writing to datastores on remote runs. Previously, if the AML Run Token is updated in Python, the Data Prep runtime will not be updated with the updated AML Run Token.
- Additional clearer error messages
- to_spark_dataframe() will no longer crash when Spark uses Kryo serialization
- Value Count Inspector can now show more than 1000 unique values
- Random Split no longer fails if the original Dataflow doesn’t have a name  

### 2018-11-19 (version 0.5.0)

New features
- Created a new DataPrep CLI to execute DataPrep packages and view the data profile for a dataset or dataflow
- Redesigned SetColumnType API to improve usability
- Renamed smart_read_file to auto_read_file
- Now includes skew and kurtosis in the Data Profile
- Can sample with stratified sampling
- Can read from zip files that contain CSV files
- Can split datasets row-wise with Random Split (e.g. into test-train sets)
- Can get all the column data types from a dataflow or a data profile by calling .dtypes
- Can get the row count from a dataflow or a data profile by calling .row_count

Bug fixes
- Fixed long to double conversion 
- Fixed assert after any add column 
- Fixed an issue with FuzzyGrouping, where it would not detect groups in some cases
- Fixed sort function to respect multi-column sort order
- Fixed and/or expressions to be similar to how Pandas handles them
- Fixed reading from dbfs path.
- Made error messages more understandable 
- Now no longer fails when reading on remote compute target using AML token
- Now no longer fails on Linux DSVM
- Now no longer crashes when non-string values are in string predicates
- Now handles assertion errors when Dataflow should fail correctly
- Now supports dbutils mounted storage locations on Azure Databricks

### 2018-11-05 (version 0.4.0)

New features
- Type Count added to Data Profile
- Value Count and Histogram is now available
- More percentiles in Data Profile
- The Median is available in Summarize
- Python 3.7 is now supported
- When you save a dataflow that contains datastores to a Data Prep package, the datastore information will be persisted as part of the Data Prep package
- Writing to datastore is now supported
 
Bug fixes
- 64bit unsigned integer overflows are now handled properly on Linux 
- Fixed incorrect text label for plain text files in smart_read
- String column type now shows up in metrics view
- Type count now is fixed to show ValueKinds mapped to single FieldType instead of individual ones
- Write_to_csv no longer fails when path is provided as a string
- When using Replace, leaving “find” blank will no longer fail

## Datasets License Information

IMPORTANT: Please read the notice and find out more about this NYC Taxi and Limousine Commission dataset here: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml 

IMPORTANT: Please read the notice and find out more about this Chicago Police Department dataset here: https://catalog.data.gov/dataset/crimes-2001-to-present-398a4 

