---
title: 修复 Windows 10 频繁断网的问题
abbrlink: d7104bdd
date: 2026-06-07 14:46:20
tags:
categories:
---

打开 “Windows PowerShell（管理员）”，依次执行下方的 5 条命令，执行完毕后重启设备：

<!--more-->

```powershell
netsh winsock reset
```

```powershell
netsh int ip reset
```

```powershell
ipconfig /release
```

```powershell
ipconfig /renew
```

```powershell
ipconfig /flushdns
```

>https://learn.microsoft.com/zh-cn/answers/questions/3807357/win10