---
title: 在 VSCode 中配置 Java 开发环境
date: 2025-02-21 21:05:33
tags: Visual Studio Code
categories:
---


# 插件安装

首先安装几个必备的插件。

1. `Extension Pack for Java`
2. `Spring Boot Extension Pack`

<!--more-->

# 环境配置

| 设置 id | 描述 | 示例值 |
| --- | --- | --- |
| java.jdt.ls.java.home | 指定用于启动 Java 语言服务器的 JDK（21 或更高版本）的文件夹路径。此设置将替换 Java 扩展内置的 JRE 以启动 Java 语言服务器。 | D:\Java\25
| java.configuration.maven.userSettings | maven 用户 settings.xml 文件的路径。 | D:\maven3\conf\settings.xml |
| java.configuration.maven.globalSettings | maven 全局 settings.xml 文件的路径。 | D:\maven3\conf\settings.xml |
| maven.settingsFile | 指定 maven 配置文件的绝对路径。 | D:\maven3\conf\settings.xml |
| maven.executable.path | 指定 mvn 可执行文件的绝对路径。 | D:\maven3\bin\mvn |
| maven.terminal.useJavaHome | 如果此值为 true ，并且配置项 java.home 具有值，则在创建新的终端窗口时，将环境变量 JAVA_HOME 设置为 java.home 的值。 | true |
| java.maven.downloadSources | 启用/禁用在导入 Maven 项目时下载依赖源码。 | true |

# 开发体验配置

## 提示忽略大小写

```
vscode://settings/java.completion.matchCase
```