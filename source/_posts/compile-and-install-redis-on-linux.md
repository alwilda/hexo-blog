---
title: Linux 下编译安装 Redis
date: 2023-05-14 17:40:07
tags:
 - Linux
 - Redis
categories:
---

首先进入官网 [Download | Redis](https://download.redis.io/releases/) 下载安装包。

<!--more-->

# 安装

解压后进行编译

```shell
# 安装到 /usr/local/redis 目录
make PREFIX=/usr/local/redis install
```

# 命令

启动：

```bash
/usr/local/redis/bin/redis-server /usr/local/redis/redis.conf
```

通过 cli 连接：

```bash
redis-cli -h host -p port -a password
```

# 服务

```bash
sudo groupadd redis 
sudo useradd -r -g redis -s /bin/false redis 
sudo chown -R redis:redis /usr/local/redis /data/redis
```

```bash
vim /etc/systemd/system/redis.service
```

{% codeblock redis.service lang:ini %}
[Unit]
Description=Redis In-Memory Data Store
After=network.target
 
[Service]
User=redis
Group=redis
Type=forking
ExecStart=/usr/local/redis/bin/redis-server /data/redis/redis.conf
ExecStop=/usr/local/redis/bin/redis-cli -p 8379 shutdown
Restart=no
  
[Install]
WantedBy=multi-user.target
{% endcodeblock %}

刷新服务：`systemctl daemon-reload`

- 关闭 redis：`systemctl stop redis`
- 开启 redis：`systemctl start redis`
- 查看 redis：`systemctl status redis`
- 自启 redis：`systemctl enable redis`