---
title: Windows安装nodejs的一些配置
author: kinglyq
tags:
- nodejs
categories: []
date: 2019-08-06 20:15:58
---
#  Windows安装nodejs

## 一 建立目录
1. 在安装nodejs的目录下新建【node_global】及【node_cache】这两个文件夹

## 二 配置这啥
2. 打开命令窗口输入：
```shell
npm config set prefix "xxx\nodejs\node_global"
npm config set cache "xxx\nodejs\node_cache"
```

<!--more-->

## 三 配置环境变量
### (一) 系统变量
```
NODE_PATH: "某盘\nodejs\node_global\node_modules" // 再建一个node_modules目录
Path: "某盘\nodejs\"
```
### (二) 用户变量
```
Path: "某盘\nodejs\node_global"
```

- 之所以这样配置是因为包被放到了node_global，如果系统变量Path指向 *"xxx\nodejs\node_global"*，可`node_global`并没有nodejs的脚本，故不识别node、npm命令，而在用户变量设置*"xxx\nodejs\node_global"*，是为了使用里面包的一些命令。比如俺就是在执行`hexo g`的时候发现的😂。

##  四 测试，没必要
```shell
npm install express -g # -g是全局安装的意思
```
