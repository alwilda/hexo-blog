---
title: 常用 cmd 命令
date: 2023-05-01 19:21:24
tags: CMD
categories:
---

- 查询端口号

```
netstat -ano|findstr 8080 
```

- 查询进程

```
tasklist|findstr 进程ID
taskkill /pid 进程ID-t -f
```