---
title: Data Modeling
layout: blog
order: 4
topic: Databases
topic_path: /docs/databases/index.html
---
Let's first think about how to isolate our data model within the postgres cluster. The postgres primitive is a database - a postgres cluster contains one or more databases. We will create a separate database for our data model.

To follow along, configure the following 
* a remote postgres cluster
* a local installation of the [psql terminal](https://www.postgresql.org/docs/current/app-psql.html)

## psql connection strings
Psql uses [libpq](https://www.postgresql.org/docs/9.5/libpq.html) to open connections between the client and the postgres cluster. Postgres clusters are specified by [connection strings](https://www.postgresql.org/docs/15/libpq-connect.html#LIBPQ-CONNSTRING). Each connection string needs to include the following :
* `host` - FQDN for the postgres host
* `port` - the default postgres port is 5432
* `user` - used for defining RBAC

Store the postgres credentials as environment variables.
```
export PG_HOST = xxxx.rds.amazonaws.com
export PGPASSWORD = mypassword
```

Open a connection for the `postgres` user
```
psql -U postgres -h $PG_HOST -p 5432
```

## Create database

Create a database
```
CREATE DATABASE workout;
```

## Database users

Connections with a postgres cluster are defined by a user. Users can be granted access to databases, schemas, and even certain commands. Close your psql connection and open a new connection with the `workout` database. 
```
psql -U postgres -h $PG_HOST -p 5432 -d workout
```

Create an admin user, and a user
```
CREATE USER workout_admin WITH PASSWORD 'password';
CREATE USER workout_user WITH PASSWORD 'password';
```

Grant access to the user. Restricting access to a set of DML statements (SELECT, INSERT, UPDATE, DELETE) is good security practice.
```
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO workout_admin;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO workout_user;
```