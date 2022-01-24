# How to Fix Insert Pandas Dataframe from Db2 issue on Cloud Pak for Data Notebook

## Issue

There is a recent issue with Cloud Pak for Data's Jupyter Notebook. When you try to insert Pandas DataFrame from a DB2 connection, it adds the code snippet however, running the code snippet will give an error.

![error](https://user-images.githubusercontent.com/52746337/150765573-9a1b2827-d620-4aad-8b41-35b36547d6a3.gif)

```python
ProgrammingError: ibm_db_dbi::ProgrammingError: [IBM][CLI Driver] SQL10013N  The specified library "GSKit Error: 2" could not be loaded.  SQLSTATE=42724 SQLCODE=-10013
```

## Solution/Workaround

This issue is caused because the SSL Certificate is base 64 encoded. 

![before](https://user-images.githubusercontent.com/52746337/150767104-69ccf04a-7ea3-433e-86c4-17b1dda0bad6.png)

You will have to decode the SSL Certificate in order to authenticate with Db2.

- You can decode the base64 encoded string in just 2 steps:
  - Import `base64` and copy the base64 encoded ssl certificate into a variable
  
    ```python
    import base64
    certificate = <Your ssl certificate>
    ```
    ![copycertificate](https://user-images.githubusercontent.com/52746337/150771080-89b13cae-0054-4cb9-8649-283605e48b5d.gif)
  - Decode base64 string into `bytes` and decode the bytes into `ascii`. Write the decoded ssl certificate to the file.
    
    ```python
    ssl_certificate_bytes = base64.b64decode(certificate)
    ssl_certificate = ssl_certificate_bytes.decode('ascii')
    
    ...
    
    f.write(ssl_certificate)
    ```
    ![sslcert](https://user-images.githubusercontent.com/52746337/150771778-6e12619b-4b0a-4ea3-8ba5-30af117c05c9.gif)

Once you have incorporated these changes you can run the code block and the Pandas DataFrame will be loaded with the Db2 table.

![errorsolved](https://user-images.githubusercontent.com/52746337/150771914-e7e6dae2-6dff-404e-ac2f-f4c4ba12bc9b.gif)

