---
title: postgres
layout: blog
order: 2
topic: Databases
topic_path: /docs/databases/index.html
---
PostgreSQL is a powerful relational database. Relational databases offer a wealth of performance advantages over file-based data storage.

# CLI Cheat Sheet
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
user-# \dt
```
Quit CLI
```bash
user-# \q
```


# Start and Stop Server
The following commands can be used to start and stop the Postgres server, and check the status of the server.
```bash
sudo service postgresql start
sudo service postgresql stop
sudo service postgresql restart
sudo service postgresql status
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