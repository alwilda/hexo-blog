---
title: 修复 Windows 任务栏 Wi-Fi 图标消失的问题
abbrlink: f3c2efb
date: 2026-02-27 19:56:39
tags:
categories:
---

使用自动系统扫描：

以管理员身份打开 `Microsoft Powershell`，逐一输入以下指令：

<!--more-->

```powershell
Dism /Online /Cleanup-Image /CheckHealth
```

```powershell
Dism /Online /Cleanup-Image /ScanHealth
```

```powershell
Dism /Online /Cleanup-Image /RestoreHealth
```

```powershell
sfc /scannow
```

重启电脑，如果出现“有一些文件无法修复”的回报，重复步骤 1-3 几次。[^1]

[^1]: [win10任务栏wifi图标消失](https://learn.microsoft.com/zh-cn/answers/questions/3251200/win10-wifi)