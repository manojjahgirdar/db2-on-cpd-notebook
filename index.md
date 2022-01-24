# How to Fix Insert Pandas Dataframe from Db2 issue on Cloud Pak for Data Notebook

## Issue

There is a recent issue with Cloud Pak for Data's Jupyter Notebook. When you try to insert Pandas Dataframe from a DB2 connection, it adds the code snippet however, running the code snippet will give an error.

```python
ProgrammingError: ibm_db_dbi::ProgrammingError: [IBM][CLI Driver] SQL10013N  The specified library "GSKit Error: 2" could not be loaded.  SQLSTATE=42724 SQLCODE=-10013
```

## Solution/Workaround

This issue is caused because the SSL Certificate is base 64 encoded. You will have to decode the SSL Certificate in order to authenticate with Db2.
