---
title: docker安装并使用MySQL57
author: kinglyq
tags:
categories: []
date: 2019-8-2 20:12:48
---
# 一 下载MySQL57
```shell
docker pull mysql:5.7
```

<!--more-->

# 二 启动

- 后台启动并设置端口号，把数据库具体的数据放在本机而不是容器内部

```shell
docker run -p 3306:3306 --name docker-mysql -v /root/docker/mysql57/conf:/etc/mysql/conf.d -v /root/docker/mysql57/logs:/logs -v /root/docker/mysql57/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7
```

# 三 从docker进入MySQL，没必要
```shell
docker exec -it docker-mysql bash

mysql -u root -p
```