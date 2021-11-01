---
layout: blog
title: Commands
order: 4
topic: Analytics
topic_path: /docs/analytics/index.html
---
Notes from using Airflow on Mac OS, with Python 3.9.7.

Install airflow
```bash
pip3 install apache-airflow
```

Uninstall airflow
```bash
pip3 uninstall apache-airflow
```

Show installation location
```bash
pip3 show apache-airflow
```

Verify airflow installation
```bash
airflow version
```

Initialize database
```bash
airflow db init
```

List active dags
```bash
airflow dags list
```

Print tasks in "tutorial" DAG
```bash
airflow tasks list tutorial
```

Print hierarchy of tasks in "tutorial" DAG
```bash
airflow tasks list tutorial --tree
```

## Setup
Create a new user
```bash
# create an admin user
airflow users create \
    --username admin \
    --firstname Peter \
    --lastname Parker \
    --role Admin \
    --email spiderman@superhero.org
```
