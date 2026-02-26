---
title: MyBatis 支持的 JDBC 类型
tags: MyBatis
abbrlink: 91bf2bed
date: 2021-03-16 09:01:12
---

只需要在可能执行插入、更新和删除的且允许空值的列上指定 `JDBC` 类型，这是 `JDBC` 的要求而非 `MyBatis` 的要求。如果你直接面向 `JDBC` 编程，你需要对可以为空值的列指定这个类型。

<!--more-->

**`JDBC` 要求，如果一个列允许使用 `null` 值，并且会使用值为 `null` 的参数，就必须要指定 JDBC 类型（`jdbcType`）。**

但大多时候，你只须简单指定属性名，顶多要为可能为空的列指定 `jdbcType`。

|            |           |               |                 |           |             |
| ---------- | --------- | ------------- | --------------- | --------- | ----------- |
| `BIT`      | `FLOAT`   | `CHAR`        | `TIMESTAMP`     | `OTHER`   | `UNDEFINED` |
| `TINYINT`  | `REAL`    | `VARCHAR`     | `BINARY`        | `BLOB`    | `NVARCHAR`  |
| `SMALLINT` | `DOUBLE`  | `LONGVARCHAR` | `VARBINARY`     | `CLOB`    | `NCHAR`     |
| `INTEGER`  | `NUMERIC` | `DATE`        | `LONGVARBINARY` | `BOOLEAN` | `NCLOB`     |
| `BIGINT`   | `DECIMAL` | `TIME`        | `NULL`          | `CURSOR`  | `ARRAY`     |
