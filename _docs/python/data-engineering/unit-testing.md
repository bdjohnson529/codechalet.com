---
layout: blog
title: SQL Unit Testing
topic: data-engineering
order: 2
parent: Python
parent_path: python/
---
All software teams face the common challenge of adding code to a source code base without breaking the code which already exists. Software engineers have traditionally solved this problem by executing unit tests which are run before new code is deployed to production. The unit tests verify that each "unit" of code executes properly.

Python has its own [unit testing framework](https://docs.python.org/3/library/unittest.html), consisting of [assertions](https://docs.python.org/3/library/unittest.html#assert-methods) which can be used to test the validity of Python code. The basic unit of testing, a test case, is a section of code which is executed and returns a value. The return value of the test case is evaluated against an expected value; if the return value equals the expected value, the test case passes. However, if the return value differs from the expected value, the test case fails.

Our source code is used to transform tables in SQL - the output of our code is a collection of tables in SQL. In our case, the goal of our unit tests was to validate the data in our SQL tables, rather than to validate the functionality of our Python code. Specifically, we used the concept of unit testing to validate the following attributes of our output tables in SQL:

* Table exists
* Table has at least one row of data
* SQL query evaluates to an empty set
* SQL query evaluates to a non-empty set


### **Table Exists**
The output data model, in our case, was a number of different SQL tables. To validate that all these tables exist, we queried the `INFORMATION_SCHEMA` of our SQL database. Speficially, we wrote a function which took a list of tables as an input. If all tables were represented, the function returns `True`, otherwise, the function returns `False`.

```sql
SELECT  TABLE_NAME
FROM    INFORMATION_SCHEMA.TABLES
WHERE   TABLE_TYPE = 'BASE TABLE'
```

### **Table has data**
In a similar manner, we can query the SQL database to return a list of tables that have at least 1 row of data. We constructed a function which took a list of tables as an input. The function returns `True` if all the tables have at least 1 row of data, and `False` otherwise.

```sql
      SELECT T.NAME      AS TABLE_NAME,
             SUM(P.rows) AS NumRecords
        FROM sys.tables     T
  INNER JOIN sys.indexes    I ON T.OBJECT_ID = I.OBJECT_ID
  INNER JOIN sys.partitions P ON I.OBJECT_ID = P.OBJECT_ID AND I.index_id = P.index_id
       WHERE I.index_id <= 1
    GROUP BY T.NAME
      HAVING SUM(P.rows) > 0
    ORDER BY SUM(P.rows) DESC
```

### **Custom SQL Queries**
We borrowed the concept of assertions from Python unit tests to construct SQL assertions, which compare the result of a SQL query to an expected result. The most basic construction of a SQL assertion is a query that evaluates to an emtpy table. Suppose that the column AmountPaid is always positive. The below query should return an empty table.

```sql
-- expect empty

SELECT TOP 10 *
FROM  		database.dbo.table
WHERE		AmountPaid < 0
```

We could also construct a query which we expect to return a non-empty table. For example, suppose we want to verify that a client is represented within a table. The below query should return a table with 10 rows.

```sql
-- expect full

SELECT TOP 10 *
FROM  		database.dbo.table
WHERE		Client = 'Mercedes'
```

Ideally, these queries would be exected by a Python function so that it can be automatically executed. In order to distinguish between the two types of queries outlined above, we add *frontmatter* to our SQL queries. The Python function responsible for executing the custom SQL queries can read the frontmatter and identify which type of assertion should be applied.

In the above queries, the first line is a comment which is not executed by the SQL interpreter. We can use Python to parse the comment and identify the expectation value of the SQL query. In our implementation, we use [regex](https://docs.python.org/3/library/re.html) to parse the frontmatter.

```python
with open(file, 'r') as f:
	test = os.path.split(file)[1]
	test_type = re.search(r'(?<=expect )\\w+', file).group(0)

	if(test_type =='full'):
		assertFull(file)
	if(test_type =='empty'):
		assertEmpty(file)
```

### **Advanced Custom Queries**
Any test case can be reduced to an assertion. For example, if we wanted to ensure that two tables had the same number of records, we could write a query to compare the `COUNT` of records in two tables.

```sql
-- expect 1

SELECT
    CASE WHEN (SELECT COUNT(*) FROM TableA) = (SELECT COUNT(*) FROM TableB)
        THEN 1
        ELSE 0
    END
``` 

The idea of embedding metadata in comments opens a world of possibilities - you could build tests which are expected to return certain values, or a certain number of rows. We have found that automating unit tests has decreased the downtime of our production datasets by 10X and increased the number of pull requests per week by a similar increment.