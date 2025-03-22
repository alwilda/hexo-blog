---
title: 清理下载失败的 maven 依赖文件
date: 2025-03-22 19:33:21
tags:
categories:
---

# Windows 脚本

<!--more-->

```shell
chcp 65001
set REPOSITORY_PATH=D:\Maven\mavenStore
rem 正在搜索...
for /f "delims=" %%i in ('dir /b /s "%REPOSITORY_PATH%\*lastUpdated*"') do (
    del /s /q %%i
)
rem 搜索完毕
pause
```
