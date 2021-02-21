---
title: 修改为阿里yum源-mirrors.aliyun.com
author: kinglyq
tags:
categories: []
date: 2019-8-1 14:12:11
---
# 一 修改为阿里yum源 -mirrors.aliyun.com

##　(一) 首先备份系统自带yum源配置文件/etc/yum.repos.d/CentOS-Base.repo

```shell
[root@localhost ~]# mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

<!--more-->

## (二) 查看CentOS系统版本
```shell
[root@localhost ~]# lsb_release -a
```
 

## (三) 下载ailiyun的yum源配置文件到/etc/yum.repos.d/
```shell
CentOS7

[root@localhost ~]# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

CentOS6

[root@localhost ~]# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo

CentOS5

[root@localhost ~]# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```


##　(四) 运行yum makecache生成缓存
```shell
[root@localhost ~]# yum makecache
```
 

## (五) 这时候再更新系统就会看到以下mirrors.aliyun.com信息
```shell
[root@localhost ~]# yum -y update
已加载插件：fastestmirror, refresh-packagekit, security
设置更新进程Loading mirror speeds from cached hostfile
* base: mirrors.aliyun.com
* extras: mirrors.aliyun.com
* updates: mirrors.aliyun.com
```