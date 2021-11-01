---
layout: blog
title: Uploading Application Code
order: 2
topic: Analytics
topic_path: /docs/analytics/index.html
---
This is a design document, explaining how to upload application code to Spark nodes, via Databricks Connect.

## Application Code

Application code, such as model definitions and helper functions, should be defined within a folder which is isolated from the runtime program. I've found it helpful to organize all the application code within a folder named application. Within the application folder, you can separate your code into folders which are more specific. For example, I usually create a folder for models, another one for helper functions, and another for pipelines.

You'll also need a file to install the Anaconda environment for that specific job, and another file for the Python package requirements.
```
├── myjob
|   ├── application
|       ├── models
|       ├── helpers
|       ├── pipelines
├── run.py
├── install.bat
├── requirements.txt
```

## Runtime Code

The file run.py contains the runtime program. This program has several responsibilities:

1. Instantiate a connection to the Spark cluster
2. Ship the application code to the Spark cluster
3. Plan the Spark job
4. Distribute the Spark job to the cluster nodes

#### Instantiate Cluster Connection

Before you execute the job, you'll need to create a [Spark session](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.SparkSession.html). The Spark session is the entry point for Pyspark. Keep in mind the Spark session will be connected to the cluster via Databricks Connect. To successfully instantiate the Spark session, you must have already configured Databricks connect on your machine. Let's create a Spark session.

```python
from pyspark.sql import SparkSession

def main():
    spark = SparkSession.builder.appName('temp').getOrCreate()

if __name__ == '__main__':
    main()
```

#### Ship Application Code

So far our program is quite simple. The next thing we need to do is ship our application code to the Spark cluster. We will use [SparkContext](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.SparkContext.html) to accomplish this goal. The SparkContext API includes a function [addPyFile](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.SparkContext.addPyFile.html), which can be used to add a `.py` or `.zip` dependency to all tasks executed within the context.

When you add a file to the SparkContext, it is shipped to the Databricks cluster and each of the worker nodes. We could add each individual Python file to the Spark context, or we could create a `.zip` archive of the application code and ship that. The `.zip` archive will be compressed, so in theory the upload time will be faster. Make sure to add `application.zip` to the `.gitignore` so it is not inadvertently added to source control.

```python
import shutil
from pyspark.sql import SparkSession
 
def main():
    spark = SparkSession.builder.appName('temp').getOrCreate()
 
    # upload the application code
    shutil.make_archive('application', 'zip', '.')
    spark.sparkContext.addPyFile('application.zip')
```

Now we can write our code which executes within the SparkSession! Since we have shipped the application code to the cluster, the cluster nodes each have a copy of the functions and modules in the application folder.