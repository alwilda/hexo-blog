---
title: Getting Started with JavaFX 11+
date: 2021-03-05 15:48:56
tags: JavaFX
categories:
---

JavaFX 允许您使用高度可移植的，现代化的，硬件加速的用户界面来创建 Java 应用程序。

<!--more-->

# 安装环境

`JavaFX` 建立在 `JDK` 之上，并且是一个独立的组件。有两种不同的选项可用于开发 `JavaFX` 应用程序：

1. 使用 `JavaFX SDK`（在 Java 11 LTS 和 15 进行选择）。
2. 使用构建系统（例如 Maven / Gradle）从 Maven Central 下载所需的模块（在上述相同版本之间进行选择）。

## Java

至少 Java 11 的版本，`Oracle JDK` 或 `Open JDK`，点击下方链接选择下载。

1. [Oracle JDK](https://www.oracle.com/cn/java/technologies/javase-downloads.html)
2. [Open JDK](https://adoptopenjdk.net/)

## JavaFX

访问 [JavaFX - Gluon](https://gluonhq.com/products/javafx/) 选择合适的版本进行下载，建议 15.0.1，这与 `Scene Builder` 的版本一致。

## Scene Builder

> Scene Builder 是面向设计的替代方案，可以提高生产率。

访问 [Scene Builder - Gluon](https://gluonhq.com/products/scene-builder/) 选择 15.0.1 版本下载安装。

# 在 IDEA 中使用

1. 新建项目时选择 `Java FX`

{% asset_img new-javafx-project.jpg 新建项目时选择JavaFX %}

2. 添加 `Java FX` 依赖：

选择 `File` -> `Project Structure` -> `Libraries` -> `+` -> `Java`

选择好目录后将其添加进项目。

{% asset_img add-javafx-lib.jpg 添加依赖 %}

3. 设置如下 `VM options`

```
--module-path ${PATH_TO_FX} --add-modules javafx.controls,javafx.fxml
```

`PATH_TO_FX` 即为 JavaFX lib 的路径，这个变量可以配置在系统中也可以配置在`IDEA`上，亦或直接写上路径。

配置如下图所示：

- VM options
  点击 `Modify options` 勾选 `Add VM options`

{% asset_img app-vm-opitons.jpg IDEA-JavaFX-VM-options %}

- 在 IDEA 中配置 `PATH_TO_FX`

{% asset_img javafx-path.jpg 在IDEA中配置PATH_TO_FX %}

4. 运行 `main` 函数，效果如图

{% asset_img n-run-r.jpg 普通javafx项目效果 %}

# 在 Maven 中使用

1. 创建项目

使用如下的 `Maven` 命令创建 `Java FX` 项目：

```
mvn archetype:generate \
        -DarchetypeGroupId=org.openjfx \
        -DarchetypeArtifactId=javafx-archetype-simple \
        -DarchetypeVersion=0.0.3 \
        -DgroupId=包名 \
        -DartifactId=项目名 \
        -Dversion=1.0.0 \
        -Djavafx-version=本地Java版本，如 11、12、。。。
```

后续也可将 `archetype` 添加到 `IDEA` 中

{% asset_img idea-javafx-archetype.jpg javafx-archetype %}

2. 项目结构

注意框起来的部分，一定要与本地安装的 `Java` 版本保持一致。

{% asset_img m-j-structure.jpg 项目结构 %}

3. 运行结果

运行 `App.java` 的 `main` 函数，效果如图所示：

{% asset_img mvn-javafx-result.jpg 效果 %}

# Scene Builder 的使用

`View` -> `Show Sample Controller Skeleton`
