---
title: 获取本机win10的产品密钥
date: 2021-03-21 09:14:06
tags: Windows
categories:
---

如何查看本机 `win10` 的产品密钥呢？👇

<!--more-->

1. 按 `win + q` 或 `win + r`，搜索 `regedit` 进入注册表。

2. 地址栏输入并进入该条目

   ```
   计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform
   ```

3. 进入 `SoftwareProtectionPlatform` 的详情页面后，打开 `BackupProductKeyDefault`，里面的数值数据就是激活密钥。
