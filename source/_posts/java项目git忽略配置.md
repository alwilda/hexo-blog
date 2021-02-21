---
title: java项目git忽略配置
author: kinglyq
tags: []
categories: []
date: 2019-7-13 16:56:09
---

实际上是从 https://start.spring.io/ 上的 *.gitignore*文件而来...

<!--more-->

```
HELP.md
target/
!.mvn/wrapper/maven-wrapper.jar
!**/src/main/**
!**/src/test/**

### STS/eclipse ###
.apt_generated
.classpath
.factorypath
.project
.settings
.springBeans
.sts4-cache

### IntelliJ IDEA ###
.idea
*.iws
*.iml
*.ipr

### NetBeans ###
/nbproject/private/
/nbbuild/
/dist/
/nbdist/
/.nb-gradle/
build/

### VS Code ###
.vscode/

```