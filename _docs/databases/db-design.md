---
title: Database Design
layout: blog
order: 4
topic: Databases
topic_path: /docs/databases/index.html
---
We recently needed to design a postgres database with performant read times for 20B records. Past attempts at designing the database had failed because the read times were exceedingly slow. After doing some research, I was able to come up with an approach which facilitated an effective design.

### Optimization constraint
I found it helped to identify a constraint which drives the database design. Since the database was the backend of a web app, we wanted our read times to be small. I identified read times as our driving constraint. We didn't actually care about write times (of course, as long as they remained below a reasonable threshold).

### Generalized use case
I then defined a generalized query which represented the most common use case. In our case, we the query was a simple select.
```sql
SELECT *
FROM TimeseriesDB
WHERE Customer = 1001
```

This query was intended to return 17,520 records.

# Indexing scheme
When the server receives the above query, it needs to identify all records which belong to Customer 1001. The least computationally efficient way of accomplishing this goal would be to iterate through all records in the database, and select the records where Customer is equal to 1001.

Of course, we have indexes to help us solve this problem. By default, Postgres uses B-tree indexes as its indexing structure. B-tree indexes are essentially binary trees with a depth of O(log n). If our database contains 1M customers, Postgres will be able to find the records of a given customer with no more than 14 traversals of the index (log 1M = 13.8).

The simple solution is to create an index on Customer.

# Data denormalization
When databases are designed to optimize write times, or to optimize space, often they will be denormalized. Let’s say Customer is a 16 character string. If we have 10k records for each customer, a more efficient way to store the records is to save customer as a numeric value, and create a different table to map the numeric value to a string.

The downside of normalizing data is that read times will increase. When you select the records for a given customer, you will need to perform a join of the numeric customer value to the normalization table.

Since we were optimizing read times, we wanted to de-normalize the data, and save the data exactly as it will be read. That way, the computation on read will be minimized.

# Database specificity
This database is optimized for the particular purpose of serving as the backend of the Django application. The reason it would be fast is because we are only storing the data which we would be rendering in the application.

Specifically, we wanted to avoid storing all historical data in the database, because then we would add another computation which the DB needs to perform on read. If we stored all historical data, and then needed to select the most recent two years, our query would transform from
```sql
SELECT  *
FROM    TimeseriesDB
WHERE   Customer = 1001
```
to
```sql
SELECT      TOP 17520 *
FROM        TimeseriesDB
WHERE       Customer = 1001
ORDER BY    Timestamp DESC
```
And we would slow down our read times. To this point, we should avoid creating a general-purpose timeseries database, and rather, create DBs which are designed for specific use cases.

# Scaling
Once the DB reaches capacity, we can scale the solution by sharding our data across several servers. For example, let’s say we experimentally determine that our DB can only work effectively for 1M customers. If we have 3M customers total, we can shard our data into 3 sister databases, and create a very simple API to route the request to the appropriate database.