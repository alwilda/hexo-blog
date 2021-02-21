---
title: idea配置tomcat以及运行普通web项目
author: kinglyq
tags:
- idea
categories: []
date: 2019-07-07 14:43:21
---
# Tomcat的配置

## 1. 在主界面打开设置

<!--more-->

![](img-1.jpg)

## 2. 选择Application Servers后点击 **+** 加号，选择Tomcat Server

![](img-2.png)

## 3. 选择tomcat的路径

![](img-3.png)

- 配置成功。

# 运行普通web项目

## 控制台乱码问题的解决办法

1. 设置idea的默认项目编码

![](img-4.jpg)

2. 配置项目中tomcat的编码

    - 打开项目界面右上方选择TomCat再选择修改

    ![](img-5.jpg)

    - 在VM options填写-Dfile.encoding=UTF-8

    ![](img-6.jpg)

3. 要是还不行就修改idea的一些配置文件

    - 打开idea安装目录下的bin文件夹
    - 打开idea.exe.vmoptions和idea64.exe.vmoptions文件
    - 添加 -Dfile.encoding=UTF-8

     ![](img-7.jpg)

