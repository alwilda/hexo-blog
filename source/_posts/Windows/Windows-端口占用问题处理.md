---
title: Windows 端口占用问题处理
abbrlink: 543f7b9f
date: 2026-05-11 20:23:31
tags:
categories:
---

执行以下命令查看哪些端口被系统保护了：

```shell
netsh int ipv4 show excludedportrange protocol=tcp
```

<!--more-->

重启 Web 辅助服务：

```shell
net stop winnat
```

```shell
net start winnat
```
