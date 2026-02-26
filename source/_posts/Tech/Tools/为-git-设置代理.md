---
title: 为 Git 设置代理
tags: Git
abbrlink: f0d3f2bf
date: 2024-08-16 21:40:04
categories:
---

# Git 使用 HTTP / HTTPS 传输协议的代理方法

```vim
git config --global http.proxy <protocol>://<host>:<port>
```

例如：

```vim
git config --global http.proxy http://127.0.0.1:9999
```