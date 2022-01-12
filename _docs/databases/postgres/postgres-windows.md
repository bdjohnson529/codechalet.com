---
title: Postgres on Windows
layout: blog
order: 2
topic: Databases
topic_path: /docs/databases/index.html
---

Postgres files are generally stored at the following location
```
C:\Program Files\PostgreSQL
```

To check the status of the server, use the Windows Services utility. To access Services,
```bash
Press Windows + R
Enter services.msc
```

## CLI Control
[pg_ctl](https://www.postgresql.org/docs/10/app-pg-ctl.html) can be used to initialize, start, stop or control a Postgres server. Note you will need to set the environment variable PGData, using the following command
```bash
set PGDATA=C:\Program Files\PostgreSQL\14\data
```

#### start
```bash
pg_ctl start
```