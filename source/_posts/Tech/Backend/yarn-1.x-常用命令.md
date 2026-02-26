---
title: Yarn 1.x 常用命令
tags: Yarn
abbrlink: 96eb1125
date: 2022-01-10 14:49:39
categories:
---

记录一些 [yarn](https://classic.yarnpkg.com) dependency management 常用的命令.....

<!--more-->

# 添加依赖

## yarn add <package...> [--dev/-D]

使用 `--dev` 或者 `-D` 将依赖安装到 devDependencies（只在开发环境下生效）中。

# 删除依赖

运行 `yarn remove 包名` 将从你的直接依赖中删除名指定名称的包，在这个过程中会更新 package.json 和 yarn.lock 文件。

# 升级依赖

## yarn upgrade [package | package@tag | package@version | --scope @scope]... [--ignore-engines] [--pattern]

该命令根据 package.json 文件中指定的版本范围，将依赖关系更新为最新版本。yarn.lock文件也将被重新创建。

可以选择指定一个或多个软件包的名称。当指定了包的名字时，只有这些包会被升级。当没有指定包的名字时，所有的依赖将被升级。

`[package]` : 当指定的包只是一个名字时，那么这个包的最新匹配版本将被升级到。

`[package@tag]` : 当指定的软件包包含一个标签时，指定的标签将被升级到。标签名称是由项目维护者选择的，通常你使用这个命令来安装一个正在开发的软件包的实验性或长期支持版本。你选择的标签将是出现在 package.json 文件中的版本。

`[package@version]` : 当一个指定的软件包包含一个版本时，那么指定的版本将被升级到。package.json的依赖关系参考也将被改变，以匹配这个指定的版本。你可以使用任何SemVer版本号或范围。

`--ignore-engines` : 这个标志可以用来跳过引擎检查。

## yarn upgrade-interactive [--latest] 显示一个选择列表

使用 `upgrade-interactive` 命令会在终端显示可升级的包列表，按 `<空格>` 选择，`<a>` 切换所有，`<i>`反转选择。

`--latest`: 这个标志告诉 yarn 忽略 package.json 中指定的版本范围，而使用注册表中标记的最新版本。

# 查看依赖

## yarn list

list 命令通过引用所有包管理器的元数据文件，包括项目的依赖关系，列出当前工作目录下的所有依赖关系。

## yarn list [--depth] [--pattern]

默认情况下，所有软件包和它们的依赖关系将被显示出来。要限制依赖关系的深度，你可以在 list 命令中加入一个标志 `--深度`，以及想要的级别。例如：

```shell
yarn list --depth=0
```

# 管理全局环境下的包

以上的命令只针对具体的一个工程，如果要管理全局环境下的包，则需要使用 `yarn global`。

`yarn global` 是一个前缀，用于一些命令，如 `add`、`list` 和 `remove`。除了使用一个全局目录来存储软件包外，它们的行为与普通版本完全一样。

例如： 
```shell
yarn global add
yarn global list --depth=0
yarn global upgrade-interactive
```

{% note danger no-icon %}
注意：与 npm 中的 --global 标志不同，global 是一个必须紧跟 yarn 的命令。输入 yarn add global package-name 将在本地添加名为 global 和 package-name 的软件包，而不是在全局添加 package-name。
{% endnote %}