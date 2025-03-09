---
title: Shiro 自定义 Realm 却只能捕获 AuthenticationException
date: 2022-03-31 21:55:22
tags: Apache Shiro
categories:
---

产生这个问题的原因可能有多种，

<!--more-->

现在笔者只遇到了一种，那就是——项目存在一个以上的 `Realm`，例如除了自定义 `Realm` 外， `resources` 目录下有个 `shiro.ini` 文件，Shiro 读取到到后自动产生了 `IniRealm`。