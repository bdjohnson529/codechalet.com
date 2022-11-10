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

## Installation on WSL
Microsoft offers a detailed guide for installing Postgres on [WSL.](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database) In addition to the steps listed on the Microsoft website, I found it necessary to complete the following steps.

The authentication config file is located at `/etc/postgresql/10/main/pg_hba.conf`, or a similar location. Change the authentication method from `peer` to `trust`. Specifically, I changed these two lines
```bash
local   all             postgres                                peer
local   all             all                                     peer
```
to these:
```bash
local   all             postgres                                trust
local   all             all                                     trust
```

Reload, and restart the server for the changes to take effect.
```bash
sudo /etc/init.d/postgresql reload
sudo service postgresql restart
```


## **External Resources**
* [Install Postgres on WSL](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)