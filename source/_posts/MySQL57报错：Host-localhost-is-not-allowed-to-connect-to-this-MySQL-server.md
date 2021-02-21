---
title: MySQL57报错：Host 'localhost' is not allowed to connect to this MySQL server
author: kinglyq
tags: 
- MySQL 
date: 2019-05-23 15:48:05
---
1. 打开my.ini（通常在C:\ProgramData\MySQL\MySQL Server 5.7  *该文件夹是默认隐藏的 *）
2. 在[mysqld]下加下面两行：
```
skip-name-resolve
skip-grant-tables
```