---
title: SQL 备忘录
date: 2023-11-02 18:17:58
tags:
categories:
---

# Oracle

- 创建用户、赋权

```sql
-- 取消 C## 开头的限制
ALTER SESSION SET "_ORACLE_SCRIPT"= TRUE;

--           用户名                 密码
CREATE USER xiaoming IDENTIFIED BY 123456;

-- 赋予连接权限 
-- CONNECT: 连接数据库、建表…… RESOURCE: 建触发器、过程……
GRANT CONNECT, RESOURCE TO xiaoming;

-- 授予对表空间 'USERS' 的权限。
ALTER USER xiaoming QUOTA UNLIMITED ON USERS;
```

- 将当前用户的某张表增删改查权限赋予另一个用户

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON Schema.TableNmae TO AnotherSchema;

-- Sequence 等同理
GRANT SELECT ON Schema.SEQ_XXX TO AnotherSchema;
```

