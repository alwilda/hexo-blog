---
title: MySQL 字符集
date: 2022-11-05 22:48:00
tags:
categories:
---

utf-8 编码可能2个字节、3个字节、4个字节的字符，但是 MySQL 的 utf8 编码只支持3字节的数据，而 utf8mb4 编码是 utf8 编码的超集，兼容 utf8，并且能存储4字节的表情字符。 

<!--more-->

# 使用 uft8mb4

查看当前字符集：

```shell
SHOW VARIABLES WHERE Variable_name LIKE 'character_set_%' OR Variable_name LIKE 'collation%';
```

<div style="width: 32rem;">
{% asset_img mysql_default_charset.png 'MySQL 默认字符集' %}
</div>

修改配置文件，一般名称为 `my.ini`，加入以下配置：

```
[client] 
default-character-set = utf8mb4 
 
[mysql] 
default-character-set = utf8mb4 
 
[mysqld] 
character-set-client-handshake = FALSE 
character-set-server = utf8mb4 
# ci 是 case insensitive, 即 "大小写不敏感"
collation-server = utf8mb4_general_ci 
init_connect='SET NAMES utf8mb4'
```

修改后重启 MySQL 服务，这时再查看发现默认字符集已经改变了。

<div style="width: 32rem;">
{% asset_img mysql_utf8mb4_charset.png 'MySQL 默认字符集' %}
</div>

# 建表语句

```
CREATE DATABASE IF NOT EXISTS test DEFAULT CHARSET utf8mb4 COLLATE utf8_general_ci;
```