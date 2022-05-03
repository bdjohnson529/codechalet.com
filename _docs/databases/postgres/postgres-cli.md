---
title: Postgres CLI
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