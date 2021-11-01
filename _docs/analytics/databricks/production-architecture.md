---
layout: blog
title: Production Architecture
order: 0
topic: Analytics
topic_path: /docs/analytics/index.html
---
If you use Databricks to execute your Spark jobs, you may wonder how to put these jobs into production. Databricks provides a nice UI for creating and editing notebooks, but what if you want to refactor these notebooks into production batch processing jobs? This article will explain how to do exactly that.

Clusters managed by Databricks can be configured with [different runtimes](https://docs.databricks.com/runtime/index.html). We will be using vanilla [Databricks Runtime](https://docs.databricks.com/runtime/dbr.html) to execute Spark. Vanilla Databricks Runtime includes Spark as well as some auxiliary libraries; for our purposes, we will mostly be using Spark.
Databricks Connect

### Spark Client Mode
Databricks Connect is a client library for Databricks Runtime. It allows you to write jobs using Spark APIs and run them remotely on a Databricks cluster instead of in the local Spark session. For example, when you run commands using Databricks Connect, the parsing and planning of the job runs on your local machine. Then, the logical representation of the job is sent to the Spark server running in Databricks for execution in the cluster.

Production Spark jobs can be run in client mode, or [cluster mode](https://spark.apache.org/docs/latest/cluster-overview.html). In client mode, the driver is launched directly within the spark-submit process which acts as a client to the cluster. The client is the machine executing the application - the local machine of the developer, or the machine where the application is deployed.

Client mode is distinguished from cluster mode, where Spark uses a cluster manager to allocate resources across applications. Cluster mode is actually preferable for a production environment: since the cluster manager is co-located with the cluster nodes, latency between the cluster manager and the worker nodes is minimized. However, cluster mode is currently not supported for standalone Python applications.