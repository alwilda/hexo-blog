---
title: Node.js 包管理器配置包缓存位置
tags:
  - npm
  - pnpm
  - yarn
abbrlink: 5dad6982
date: 2023-02-05 14:58:07
categories:
---

# npm

## 查看配置

- `npm config ls` or `npm config list` 所有配置
- `npm config list -l`
- `npm config get xxx` 获取某配置

<!--more-->

## 各种目录配置

```bash
npm config set prefix D:\...\npm\global # 全局
npm config set cache D:\...\npm\cache   # 缓存
```

# pnpm

## 查看配置

```bash
pnpm config list
```

## 各种目录配置

```bash
pnpm config set store-dir=D:\...\pnpm\store
pnpm config set state-dir=D:\...\pnpm\state
pnpm config set cache-dir=D:\...\pnpm\cache
pnpm config set global-dir=D:\...\pnpm\global
pnpm config set global-bin-dir=D:\..\pnpm\global
```

# yarn 1.x

使用 ```yarn config list```查看所有**已配置**的信息

## 改变 yarn 缓存路径

```bash
yarn config set cache-folder <path>
```

或者通过环境变量 `YARN_CACHE_FOLDER` 指定缓存目录

```bash
YARN_CACHE_FOLDER=<path> yarn <command>
```

运行 `yarn cache dir` 会打印出当前的 yarn 全局缓存在哪里

## 改变 yarn 全局安装路径

设置安装位置

```bash
yarn config set global-folder <path>
```

`yarn global bin` 输出 yarn 为您已安装的可执行文件之符号链接准备的位置，打印存放全局 *node_modules* 的全局安装文件夹，可以使用 `yarn config set prefix <filepath>` 配置此基本位置。

例如设置 *D:\Yarn\Global* 为全局安装目录为例，则配置：

1. `yarn config set global-folder D:\Yarn\Global`
2. `yarn config set prefix  D:\Yarn\Global`

`npm` 或 `pnpm` 或 `yarn` 都需要将全局路径添加到环境变量 *`PATH`* 中，方可使用全局安装的那些包的命令。

# 管理工具

## cgr 

> 同时或分开管理 npm、yarn 源的工具，用来代替 nrm

1. 安装 `npm install -g cgr`
2. 使用
   - 默认源列表: N 代表 npm，Y 代表 yarn，* 代表 npm 和 yarn 共用的源
   - 源切换: y/yarn 代表 yarn 切换，n/npm 代表 npm 切换，大小写均可，type 为空，表示同时切换源
3. 添加私有源 `cgr add 源name http[s]://xxx`
4. 删除 `cgr del 源`
5. 测试 `cgr test`

## nrm

1. 安装 `npm install -g nrm`
2. 查看所有配置的源 `nrm ls`
3. 切换源 `nrm use <registry>`
4. 添加源 `nrm add registry http[s]://xxx`
5. 删除源 `nrm del <registry>`
6. 测试响应速度 `nrm test npm`