---
title: IntelliJ IDEA 的个人配置
date: 2021-03-17 21:12:19
tags: IntelliJ IDEA
categories:
---

{% blockquote JetBrains https://www.jetbrains.com/zh-cn/idea/ IntelliJ IDEA：JetBrains %}
功能强大，符合人体工程学的 JVM IDE
{% endblockquote %}

<!--more-->
<br />

# 设置

## 字体

## Maven

## 浏览器

## JavaFX

## 关闭更新

## 自动换行

{% asset_img wrap-1.jpg 自动换行1 %}

{% asset_img wrap-2.jpg 自动换行2 %}

## 文件编码

## 关闭自动保存

{% asset_img auto-save.jpg 关闭自动保存 %}

{% asset_img star-mark.jpg 星号标记 %}

## 代码注释模板

```
/**
 * @author <a href="https://github.com/kinglyq" target="_blank">kinglyq<a/>
 */
```

## 使用 Prettier

1. 安装 [Prettier](https://plugins.jetbrains.com/plugin/10456-prettier/versions) 插件。

2. {% asset_img prettier.jpg Prettier %}

## 关闭双击 shift 搜索

~~按 `Crrl+Shift+A`，输入 `Registry`,找到 `ide.suppress.double.click.handler` 后把 ✔ 打上即可~~

在 **2021.2.1** 或之前的几个版本更新后，上面的方法已经不再适用，现在这个设置已经换到了，讷 👇

{% asset_img disable-double.jpg 关闭双击功能 %}

## 关闭提示区分大小写

`Editor` -> `General` -> `Code Completion`

## 修改注释的用户名

修改 vmoptions 文件，添加 `-Duser.name=任何名字`，然后重启 IDEA。

# 插件

1. [Rainbow Brackets](https://plugins.jetbrains.com/plugin/10080-rainbow-brackets)
