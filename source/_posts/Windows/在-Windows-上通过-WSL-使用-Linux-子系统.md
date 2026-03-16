---
title: 在 Windows 上通过 WSL 使用 Linux 子系统
abbrlink: 49a3dbed
date: 2026-03-16 14:07:59
tags:
categories:
---

{% blockquote @Microsoft https://learn.microsoft.com/zh-cn/windows/wsl/ %}
适用于 Linux 的 Windows 子系统（WSL）允许开发人员直接在 Windows 上运行 GNU/Linux 环境（包括大多数命令行工具、实用工具和应用程序），无需传统虚拟机或双启动设置的开销。
{% endblockquote %}

必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11 才能使用以下命令。 如果使用的是早期版本，请参阅[手动安装页](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)。

<!-- more -->

# 安装 Linux

默认情况下，已安装的 Linux 发行版将为 Ubuntu。 可以通过使用 `-d` 标志来更改这一点。

```bash
wsl --install -d Ubuntu
```

列出可用的 Linux 发行版：

```bash
wsl --list --online
```

首次启动 Ubuntu 时，系统会要求你设置用户名 (Username) 和 密码 (Password)。这与 Windows 账户无关，是 Linux 系统独立的权限凭证。

常用管理命令：
- 进入 Linux： 在命令行输入 `wsl`。
- 查看状态： `wsl -l -v`（查看已安装的版本和运行状态）。
- 关闭 WSL： `wsl --shutdown`（当需要彻底重启 Linux 或是释放内存时使用）。

# 集成 Docker

>在 Windows 10 上将 Docker Desktop 与 WSL 2 集成是目前最推荐的开发方式。相比传统的 Hyper-V 模式，它启动更快、占用资源更少，且能在 Ubuntu 终端里直接调用 docker 命令。
>{% note no-icon 为什么启动更快，占用资源更少 %}
>- Hyper-V 模式（旧/传统模式）： Docker 会通过 Hyper-V 启动一个完整的、重型的 Linux 虚拟机（MobyLinuxVM）。这就像你在电脑里完整地启动了另一台电脑，需要加载 BIOS、初始化虚拟硬件、启动完整的内核。通常需要 30 秒甚至更久。
>
>- WSL 2 模式（新/推荐模式）： WSL 2 使用的是微软定制的轻量级实用程序虚拟机（Lightweight Utility VM）。它在后台几乎是瞬间启动的（通常在 1-2 秒内），因为它不需要模拟完整的硬件层，而是直接与 Windows 宿主机共享内核资源。
>{% endnote %}


参考 [WSL 上的 Docker 容器入门 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/wsl-containers)

Docker Desktop 设置国内镜像：

这里使用 [阿里云容器镜像服务](https://cr.console.aliyun.com/instances/mirrors) 作为国内镜像源。

登录阿里云容器镜像服务控制台，在左侧菜单栏选择 “镜像工具” -> “镜像加速器” 即可看到专属加速器地址。
