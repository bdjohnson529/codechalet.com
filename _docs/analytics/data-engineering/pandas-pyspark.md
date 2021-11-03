---
layout: blog
title: Pandas and PySpark Dataframes
order: 3
topic: Analytics
topic_path: /docs/analytics/index.html
---
One important concept to understand when writing Spark programs in Python is the distinction between Pandas dataframes, and PySpark dataframes. Both have similar syntax, which can lead to confusion when a dataframe is missing an expected method. The easiest way to determine the object type is using the native [type function](https://www.geeksforgeeks.org/python-type-function/). For more information on each object type, please see the module documentation:

* [Pandas DataFrames](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)
* [PySpark DataFrames](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.DataFrame.html)

To distinguish between the two in our code, let's use different variable names for each type of dataframe. For Pandas dataframes, use the suffix `df`, and for PySpark dataframes, use the suffix `pdf`.

To convert from a Pandas dataframe to a PySpark dataframe, use the PySpark function [createDataFrame](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.SparkSession.createDataFrame.html). To convert from PySpark to Pandas, use the PySpark function [toPandas](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.DataFrame.toPandas.html). The code below demonstrates each function.

```python
d = {'UniqueID': [1, 1, 2, 2, 3, 3], 'Energy': [1, 2, 3, 4, 5, 6]}
df = pd.DataFrame(data=d)
pdf = self.spark.createDataFrame(df)
 
og_df = pdf.toPandas()
```