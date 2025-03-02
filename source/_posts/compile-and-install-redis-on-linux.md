---
title: Linux 下编译安装 Redis
date: 2023-05-14 17:40:07
tags:
categories:
---

首先进入官网 [Download | Redis](https://redis.io/download/) 下载安装包。

<!--more-->

# 安装

1. 解压安装包

```shell
tar -zxvf redis-7.0.11.tar.gz
```

2. 预编译

```shell
cd redis-7.0.11
make
```

3. 安装

```shell
# 安装到 /usr/local/redis 目录
make install prefix=/usr/local/redis/
```

# 加入系统服务

1. `vim /etc/systemd/system/redis.service`
2. 写入以下内容：

```
[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart= /usr/local/redis/bin/redis-server /usr/local/redis/bin/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

2. 重载系统服务：`systemctl daemon-reload`

3. 服务命令：

    - 关闭 redis-server：`systemctl stop redis.service`
    - 开启 redsi-server：`systemctl start redis.service`
    - 查看 redis-server 状态：`systemctl status redis.service`

4. 开机自启

```shell
systemctl enable redis.service 
```