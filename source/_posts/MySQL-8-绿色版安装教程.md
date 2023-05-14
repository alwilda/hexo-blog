---
title: MySQL 8.x 绿色版安装教程
date: 2023-02-12 22:35:48
tags:
categories:
---

首先，到 [MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/) 下载压缩包。

<!--more-->

1. 将下载好的压缩包解压到合适的位置并解压，解压后的位置例如在 `C:\Program Files\mysql-8.0.32-winx64`。

2. 在 `C:\Program Files\mysql-8.0.32-winx64` 下创建 `my.ini` 文件，文件内容如下：

```
[mysql]

# 设置 mysql 客户端默认字符集
default-character-set=utf8mb4

[mysqld]

# 设置3306端口
port=3306

# 设置mysql的安装目录
basedir=C:\Program Files\mysql-8.0.32-winx64\

# 设置mysql数据库的数据的存放目录
datadir=C:\Program Files\mysql-8.0.32-winx64\data\

# 允许最大连接数
max_connections=200

# 允许连接失败的次数，这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10

# 服务端使用的字符集默认为 UTF8
character-set-server=utf8mb4

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB

[client]

# 设置 mysql 客户端连接服务端时默认使用的端口
port=3306

default-character-set=utf8mb4
```
> 注意每一行配置后面不要有空格！

3. 以管理员身份运行 cmd 进入 bin 目录，并执行初始化命令：

```
mysqld --initialize --console
```

{% asset_img mysql-install-1.png MySQL-安装图例-1 %}

初始化完成后生成的用户名和密码（红框所示位置即为密码），即 root 用户和生成的密码，后续我们可以更改。

4. 执行 `mysqld --install` 安装到服务，默认服务名为 `MySQL`，启动服务命令为：`net start MySQL`，停止服务：`net stop MySQL` ，卸载服务：`sc delete MySQL`。

{% asset_img mysql-install-2.png MySQL-安装图例-2 %}

5. 登录 MySQL 然后修改 root 密码：
    1. 输入命令：`mysql -u root -p`。
    2. 键入刚才红框中的密码，此时登录成功。
    3. 输入语句 `alter user root@'localhost' identified by '123456';`，123456 即为新的密码。
    4. 输入 `exit;` 退出后，再重新登录试下新密码。

6. 将 `C:\Program Files\mysql-8.0.32-winx64\bin` 添加到环境变量 Path 中。

TODO:

```
set global validate_password.policy=LOW;
set global validate_password.length=5;
```

此时，MySQL 安装完成。 👏
