---
title: MySQL执行sql语句报错"[Err] 1055 - Expression \#1 of ORDER BY... GROUP BY clause and
author: kinglyq
tags: 
- MySQL 
date: 2019-04-07 22:21:49
---
1.  查看下SQL的模式
```
SHOW VARIABLES LIKE '%sql_mode%';  查看下SQL的模式,非必须
```

2.  修改sql_mode的值
<!--more-->
```
set sql_mode = '';
set sql_mode = 'NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES';
```

- 再次执行刚才的语句，就不会报错了。

---
1. 或者执行:
```
select version(),
@@sql_mode;SET sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```

- 这里我并没有深入研究，姑且先知道这样做能解决问题罢了。