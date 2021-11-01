---
layout: blog
title: Databricks Connect
order: 1
topic: Analytics
topic_path: /docs/analytics/index.html
---


To install DB Connect on your local machine:

1. Create a new Anaconda environment
```
conda create --name dbconnect python=3.8
conda activate dbconnect
```

2. Uninstall pyspark
```
pip uninstall pyspark
```

3. Install databricks-connect
```
pip install -U "databricks-connect==8.1.*"
```

4. Configure databricks-connect. Use the values below
```
databricks-connect configure
```

5. Test connection
```
databricks-connect test
```

## Dependencies

Pyspark will run if you install databricks-connect as the instructions above indicate. However, you will receive some warning messages indicating that there are still some dependencies which are not installed on your machine. To get rid of the winutils warning, do the following:

**Install hadoop binaries**
1. Download `hadoop-3.3.1` to your local machine, by clicking the appropriate file on the Hadoop download page. I saved the zipped file to `C:/Users/myuser/Documents/lib`
2. Unzip hadoop-3.3.1. When it is completely unzipped, you will be able to see a folder named bin. This is the location of the hadoop binaries.
3. Add the hadoop filepath to your Environment variables.
    * Add a new user variable named `HADOOP_HOME` and set the value as the filepath of the unzipped folder `hadoop-3.3.1`
    * Edit the system variable `PATH`, and the hadoop filepath to the list of `PATH` variables

**Add winutils.exe to the hadoop binaries**
1. Clone the [winutils repo](https://github.com/steveloughran/winutils) onto your machine
2. Find a winutils.exe file in one of the bin folders.
3. Copy this file to hadoop-3.3.1/bin
