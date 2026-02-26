---
title: 在 Windows 下使用命令行计算文件校验值
tags: Windows
abbrlink: 8fa9d02b
date: 2023-01-01 16:45:16
categories:
---
在 Windows 中可以使用命令 `certutil` 来计算文件的校验值。

<!--more-->

<div style="width:65%;">
{% asset_img command.png %}
</div>

通过 `certutil -hashfile -?` 可以知道它支持的哈希算法有: MD2 MD4 MD5 SHA1 SHA256 SHA384 SHA512

那么要计算一个文件的 SHA256 值则可以使用：

```shell
certutil -hashfile D:\xxx\xxx.txt SHA256
```

或者相对路径：

```shell
certutil -hashfile xxx.txt SHA256
```