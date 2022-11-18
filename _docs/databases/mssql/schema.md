---
title: Schema
layout: blog
order: 3
topic: Databases
topic_path: /docs/databases/index.html
---

These queries are tested in T-SQL on a physical SQL Server.

## Cheat Sheet

Get table schema
```sql
SELECT  table_name,
        column_name,
        data_type,
        column_default
FROM    information_schema.columns
WHERE   table_name = 'mytablename';
```