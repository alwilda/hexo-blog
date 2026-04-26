---
title: 常用 npm 命令
abbrlink: a7ee44cb
date: 2026-04-24 21:20:02
tags:
categories:
---

查看已安装的全局包及版本号：

```bash
npm -g --depth=0
```

```bash
npm list -g --depth=0 --json
```

<!--more-->

查看包可用版本：

```bash
npm view <package-name> versions
```

查看全局安装路径：

```bash
npm root -g
``` 

检查全局包更新：

```bash
npm outdated -g --depth=0
```

卸载全局包：

```bash
npm uninstall -g <package-name>
```

代理问题：

```bash
npm config set proxy http://[IP_ADDRESS]/
npm config set https-proxy http://[IP_ADDRESS]/
```

```bash
npm config get proxy
npm config get https-proxy
```

```bash
npm config delete proxy
npm config delete https-proxy
```

强制清理缓存：

```bash
npm cache clean --force
```

开启 Verbose 模式：

> 当遇到安装卡住或不明原因报错时，开启 Verbose 模式，可以排查问题。

```bash
npm install -g <package-name> --verbose
```

