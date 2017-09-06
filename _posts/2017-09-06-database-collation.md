---
layout: post
category: Database
title: Get database default collation
tagline: 2017-09-06
tags: [SQLServer]
---

Find non default collation on columns for all tables in SQL Server

<!--more-->

## 问题背景 ##

因为测试环境下有数个历史项目的数据库在某服务器上，现在重构某历史遗留程序时需要 join 若干个来自不同数据库的表。遇到了 collation 冲突的错误。之前虽然也遇到但是并没有深入研究，只是用了指定 collation 的方式规避了冲突。

### 查询当前数据库 Collation ###

[https://stackoverflow.com/questions/8488534](https://stackoverflow.com/questions/8488534)

```sql
DECLARE @DatabaseCollation VARCHAR(100)

SELECT 
    @DatabaseCollation = collation_name 
FROM 
    sys.databases
WHERE 
    database_id = DB_ID()

SELECT 
    @DatabaseCollation 'Default database collation'

SELECT 
    t.Name 'Table Name',
    c.name 'Col Name',
    ty.name 'Type Name',
    c.max_length,
    c.collation_name,
    c.is_nullable
FROM 
    sys.columns c 
INNER JOIN 
    sys.tables t ON c.object_id = t.object_id
INNER JOIN 
    sys.types ty ON c.system_type_id = ty.system_type_id    
WHERE 
    t.is_ms_shipped = 0
    AND 
    c.collation_name <> @DatabaseCollation
```

### 问题原因 ###

在上述脚本的帮助下，大致就推断倒了问题原因。因为在测试时，用了 SELECT INTO 将一数据库下的表插入到了另一个数据库中。但是这两个数据库的默认 collation 是不同的。而 SELECT INTO 的方式令新表保留了原表的 collation。
