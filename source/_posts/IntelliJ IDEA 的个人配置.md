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

`File` | `Settings` | `Edito` | `General` | `Code Completion` 

取消勾选 Match case

## 修改注释的用户名

修改 vmoptions 文件，添加 `-Duser.name=任何名字`，然后重启 IDEA。

## 代码格式化

### 解决 HTML body 下的标签无缩进

设置路径：`File` | `Settings` | `Editor` | `Code Style` | `HTML`

选择 `Other` 后，编辑 `Do not indent children of`（不缩进子集），然后去掉 *不想无缩进* 的标签就可以了。

### SQL 子查询右括号另起一行

设置路径：`File` | `Settings` | `Editor` | `Code Style` | `SQL` 选择具体的数据库或通用。

选择 `Queries` 下拉找到 `Subquery` -> `Place the closing parenthesis` 修改为 `To begin`。

### 单行注释挨着代码而不是在行首

设置路径：`File` | `Settings` | `Editor` | `Code Style` | `Java` | `Code Generation`

取消勾选 `Line comment at first column`.

{% asset_img line-comment-not-first.png 取消单行注释在行首 %}

## 生成 serialVersionUID

设置路径：`File` | `Settings` | `Editor` | `Inspections`，或直接搜索 `serialVersionUID`。

然后勾选 JVM languages 下的

- [x] Serializable class without 'serialVersionUID'

# 插件

1. [Rainbow Brackets](https://plugins.jetbrains.com/plugin/10080-rainbow-brackets)

# 代码运行配置

可以编辑配置模板 Application、 JUnit 或其它。

## log4j2 彩色日志

Add VM Options: `-Dlog4j.skipJansi=false`

## SpringBoot 单元测试彩色日志

Add VM Options: `-Dspring.output.ansi.enabled=ALWAYS`

## Jansi 彩色输出

Add VM Options: `-Djansi.passthrough=true`