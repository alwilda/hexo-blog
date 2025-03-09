---
title: 在 VSCode 中配置 Java 开发环境
date: 2025-02-21 21:05:33
tags: Visual Studio Code
categories:
---

首先安装 [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) 插件。

<!--more-->

# 环境配置

将 Java 安装路径和 Maven settings.xml 替换为实际路径即可。

```json
{
    "java.jdt.ls.java.home": "C:\\xxx\\java21",
    "java.maven.downloadSources": true,
    "java.configuration.maven.userSettings": "D:\\xxx\\apache-maven-3.9.9\\conf\\settings.xml",
    "java.configuration.maven.globalSettings": "D:\\xxx\\apache-maven-3.9.9\\conf\\settings.xml",
    "maven.settingsFile": "D:\\xxx\\apache-maven-3.9.9\\conf\\settings.xml",
    "maven.terminal.useJavaHome": true,
}
```

# 开发体验配置

## 提示忽略大小写

```
vscode://settings/java.completion.matchCase
```