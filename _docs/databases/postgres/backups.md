---
title: Backups
layout: blog
order: 5
topic: Databases
topic_path: /docs/databases/index.html
---
pg_dump is a utility for backing up a postgres database.

<hr><br>

## Commands

Create a backup of a table.
```
pg_dump --host <host> --format=directory --create --jobs 5 \
        --dbname <database> --username <username> \
        --table <tablename> --file <filename.sql>
```
