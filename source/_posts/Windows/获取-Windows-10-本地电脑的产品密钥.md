---
title: 获取 Windows 10 本地电脑的产品密钥
tags: Windows
abbrlink: 85bc518b
date: 2021-03-21 09:14:06
categories:
---

如何查看本地 Windows 的产品密钥呢？
首先进入注册表：

<!--more-->

1. 按 `win + q` 或 `win + r`，搜索 `regedit` 进入注册表。

2. 地址栏输入并进入该条目

   ```
   计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform
   ```

3. 进入 `SoftwareProtectionPlatform` 的详情页面后，打开 `BackupProductKeyDefault`，*数值数据* 就是激活密钥。
