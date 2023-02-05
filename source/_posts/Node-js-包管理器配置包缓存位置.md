---
title: Node.js 包管理器配置包缓存位置
date: 2023-02-05 14:58:07
tags:
categories:
---

# npm

## 查看配置

- `npm config ls or npm config list` 所有配置。
- `npm config list -l` 获取某配置。
- `npm config get xxx`

<!--more-->

## 配置全局安装和缓存路径

- `npm config set prefix xxxpath`
- `npm config set cache xxxpath`

> Windows 下要将全局路径添加到环境变量 PATH 中，方可使用依赖的独有命令。

## 相关命令

查看全局包：`npm list -g --depth 0`

卸载包：`npm uninstall`

# Yarn

使用 `yarn config list` 查看所有已配置的信息。

设置 `cache-folder` 来配置缓存目录。

```
yarn config set cache-folder <path>
```

或者 通过环境变量 `YARN_CACHE_FOLDER` 指定缓存目录。

```
YARN_CACHE_FOLDER=<path> yarn <command>
```

运行 `yarn cache dir` 会打印出当前的 yarn 全局缓存在哪里。

## 改变 yarn 全局安装路径

设置安装位置

```
yarn config set global-folder <path>
```

`yarn global bin` 将输出 `Yarn` 为您已安装的可执行文件之符号链接准备的位置。 您可以使用 `yarn config set prefix <filepath>` 配置此基本位置。

`yarn global dir` 将打印存放全局node_modules的全局安装文件夹。

例如：以设置 `D:\Yarn\Global` 为全局安装目录为例，则：

- `yarn config set global-folder D:\Yarn\Global`
- `yarn config set prefix  D:\Yarn\Global`

> 全局安装依赖时会将其命令脚本放到 D:\Yarn\Global\bin下，所以要将D:\Yarn\Global\bin 配置到环境变量 PATH 中。