---
title: psql CLI
layout: blog
order: 2
topic: Databases
topic_path: /docs/databases/index.html
---

Log in
```bash
psql -d mydb -U myuser
```

Root login
```bash
psql -U postgres
```

Show all tables
```bash
\dt
```

Show all schemas
```bash
\dn
```

Check version
```
select version();
```

Create schema
```bash
CREATE SCHEMA myschema;
```

Change schema
```bash
SET search_path TO myschema;
```

Quit CLI
```bash
\q
```

Export query to CSV
```
psql --dbname=mydb --username=dbuser --host=127.0.0.1 \
     -c "COPY (SELECT * FROM widget) TO stdout \
     DELIMITER ',' CSV HEADER" > export.csv
```