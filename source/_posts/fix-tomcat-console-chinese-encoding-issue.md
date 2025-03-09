---
title: 解决 tomcat 控制台中文乱码
date: 2024-06-16 15:08:41
tags: Apache Tomcat
categories:
---

编辑 `/conf/logging.properties`，将以下两个编码配置改为 `GBK`。

```properties
1catalina.org.apache.juli.AsyncFileHandler.encoding = GBK
java.util.logging.ConsoleHandler.encoding = GBK
```

<small>同时适用于使用 IntelliJ IDEA 配置 Tomcat 启动项目后控制台乱码的情况。</small>