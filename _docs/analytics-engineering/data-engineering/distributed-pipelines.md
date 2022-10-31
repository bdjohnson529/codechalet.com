---
layout: blog
title: Spark Pipelines
order: 3
topic: Analytics Engineering
topic_path: /docs/analytics-engineering/index.html
---
There are many cases when we we need to perform a computation, or some sort of processing, on a large dataset. Consider, for example, a dataset with one million rows (a modest size in the context of big data). Let's say we have a computation which takes 1 second to perform. If we run the calculation on a single processor, the calculation will take 277 hours to complete.

Distributed computing solves this problem. Just as multi-threaded programs empower parallel computations on the same processor, distributed computing empowers parallel computations on a distributed network of computers. [Apache Spark](https://spark.apache.org/docs/latest/quick-start.html) is a programming framework which facilitates distributed computing. In a nutshell, the driver program generates tasks for each one of the executors. The executors complete the assigned tasks and then send the result back to the driver.

The [Spark quickstart guide](https://spark.apache.org/docs/latest/quick-start.html) is a great place to start. This tutorial assumes a basic understanding of Spark RDDs, and familiarity with Python.


# **Pipelines as a function**
Let's say you want to build a regression which correlates a customer's energy consumption with the weather. Conceptually, building the regression for a single customer is straight forward. Two arrays are used as inputs: the energy consumption timeseries, and the weather timeseries. In Python, you could use the [`sklearn.linear_model.LinearRegression`](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) class to build a regression from the two input arrays.

Let's say we are interested in the coefficients, and the goodness-of-fit of the regression. We could write the following function to build the regression and return the desired parameters.

{% highlight python %}
def calculateLinearRegression(X, Y):
    X = np.array(X)
    Y = np.array(Y)
    
    X = X.reshape(-1,2)
    Y = X.reshape(-1,2)

    reg = LinearRegression().fit(X, Y)
    
    r_squared = round(reg.score(X, Y), 2)
    m = round(reg.coef_[0][0], 2)
    b = round(reg.intercept_[0], 2)
    
    return r_squared, m, b
{% endhighlight %}

Let's execute the function on a sample dataset.

{% highlight python %}
import numpy as np
from sklearn.linear_model import LinearRegression

X = [100, 150, 125, 115]
Y = [50, 62, 61, 52]

calculateLinearRegression(X, Y)
{% endhighlight %}
```
[0.79, 0.26, 24.58]
```

That was simple enough, but how do we build a regression for each of 1 million customers? Let's say our input data is provided in the form of two datasets - one dataset with energy consumption for all customers, and another dataset with weather data for all customers. Conceivably we could use the split-apply-combine framework to generate regression results for each customer.

1. Split the data into grouped datasets for each customer.
2. Apply the regression to each customer.
3. Combine the regression results for all customers.

Of course, there is one obstacle to this approach. In Pandas, the split-apply-combine framework is implemented by the [groupby function](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html). The `groupby` function can only be applied to a single dataframe. How are we to apply this framework to two separate datasets?

The most obvious answer is to merge the energy and the weather data into a single dataset. This approach can work in certain situations. In the above example, the X and Y arrays have the same number of elements, so a merge is entirely possible. However, there are more complex situations when you may want to generate a model based on two arrays of different lengths. How can you possibly merge two arrays of different lengths?

# **Functional input dataframes**
Let's again consider the function `calculateLinearRegression(X, Y)`. What if we built an input dataset, where each column represented one of the inputs to this function? Our dataset might look like this:

|Name | X | Y |
| :-- | :-- | :-- |
| Trevor | [100, 150, 125, 115] | [50, 62, 61, 52] |
| Cassidy | [98, 99, 115, 112] | [45, 42, 55, 60] |
| April | [128, 135, 130, 132] | [68, 66, 70, 75] |

Now we can make full use of the split-apply-combine paradigm. We can use [`pandas.DataFrame.groupby`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html) to split the input dataset into groups for each customer, and then we can apply `calculateLinearRegression` to each grouped dataset. In Pandas, it might look like this:

{% highlight python %}
input_df = pd.DataFrame([
				['Trevor', [100, 150, 125, 115], [50, 62, 61, 52]],
				['Cassidy', [98, 99, 115, 112], [45, 42, 55, 60]],
				['April', [128, 135, 130, 132], [68, 66, 70, 75]]
			],
			columns = ['Name', 'X', 'Y'])

output_df = input_df.groupby('Name').apply(lambda row: calculateLinearRegression(row['X'], row['Y']))
{% endhighlight %}

To get the code to execute, you will need to modify the `calculateLinearRegression` function to convert the pd.Series, passed in from the `apply` function, to a list.
{% highlight python %}
def calculateLinearRegression(X, Y):
    X = np.array(X.values[0])
    Y = np.array(Y.values[0])

    ...
{% endhighlight %}

# **Implementation in PySpark**
Spark 3.0.1 includes the [`applyInPandas`](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=applyinpandas#pyspark.sql.GroupedData.applyInPandas) function, which can be applied to a grouped dataset. Practically, this function takes the place of the Pandas [`apply`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html) function. `applyInPandas` passes in the grouped dataset *as a Pandas dataframe* to a Python function; user-defined or otherwise. The `applyInPandas` function then expects *another Pandas dataframe* as the return value from the applied Python function.

Previous versions of Spark relied on the [`apply`](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=apply#pyspark.sql.GroupedData.apply) function, which applies a user-defined Python function to a grouped dataset. Python functions can be factored as UDFs, but the process is not always easy. In Spark 3.0.1, the [`apply`](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=apply#pyspark.sql.GroupedData.apply) function is simply an alias of the [`applyInPandas`](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=applyinpandas#pyspark.sql.GroupedData.applyInPandas) function. It makes sense to use the core function, plus, we don't need to create a UDF to use [`applyInPandas`](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=applyinpandas#pyspark.sql.GroupedData.applyInPandas); any Python function will do.

The good news is we can use our `applyInPandas` to apply our `calculateLinearRegression` function, with minimal modification. The inputs parameters and return value of the function needs to be modified, but that is pretty much it. The function can include either one input parameter: the input dataframe, or two: the grouped key, and the input dataframe. In our case we will pull the key as well as the dataframe so that we can include the key in our output dataset. The [Spark docs](https://spark.apache.org/docs/3.0.1/api/python/pyspark.sql.html?highlight=applyinpandas#pyspark.sql.GroupedData.applyInPandas) do a great job of explaining the functionality of `applyInPandas`.

{% highlight python %}
def calculateLinearRegression(key, df):
    X = df['X'].values[0]
    X = df['Y'].values[0]

    ...

    return pd.DataFrame({'Name': [key[0]], 'RSquared': [r_squared], 'Slope': [slope], 'Intercept': [intercept]})
{% endhighlight %}

And after we build our input dataframe, we can apply our pipeline.

{% highlight python %}
output_df = input_df.groupby("Name").applyInPandas(calculateLinearRegression, schema="Name string, RSquared float, Slope float, Intercept float")
{% endhighlight %}


Voila! It really is that easy to translate pipelines from Python to Spark.

# **Further Research**
Many of our models use two or more timeseries as inputs. We want to pass in the timeseries to the modeling function, without losing any information. Two dimensional arrays can be used to store a timeseries, with one column for timestamps, and another for the measurement (temperature, energy consumption, or otherwise). We have also found that JSON strings are quite useful to store timeseries, especially with the convenient Pandas functions to convert dataframes [to](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_json.html) and [from](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_json.html) JSON.