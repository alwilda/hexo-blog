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

# 文件管理

{% tabs apt %}
<!-- tab 从资源管理器访问-->
在搜索或地址栏输入 `\\wsl$` 并打开，即可看到所有已安装的 Linux 发行版（如 Ubuntu），双击进入即可通过拖拽、复制、粘贴来传输文件。

{% note info %}
在 WSL 终端中输入 `explorer.exe .`（注意后面有个点），可以直接在当前 Linux 路径下打开 Windows 文件夹窗口。
{% endnote %}
<!-- endtab -->

<!-- tab 使用 VS Code-->
打开 VS Code，安装 WSL 扩展。

点击左下角的“远程窗口”图标，选择 Connect to WSL。

连接后，可以直接从 Windows 桌面把文件拖入 VS Code 的资源管理器侧边栏，它会自动上传到 WSL 对应的路径。
<!-- endtab -->
{% endtabs %}

# 重置系统

打开 PowerShell（管理员）执行以下命令：

```powershell
wsl --unregister Ubuntu
```

如果是在设置里重置的系统，导致报错如下错误，那么也执行同样执行一下上面的命令。

```
WSL2: 系统找不到指定的文件。
错误代码: Wsl/Service/CreateInstance/MountDisk/HCS/ERROR_FILE_NOT_FOUND
```

# 使用本地代理

以 v2ray 为例：

1. 在 v2rayN 参数设置里启用 “允许来自局域网的连接”。
2. 获取 Windows 宿主机 IP 并设置环境变量。

```bash 
# 获取宿主机 IP
export hostip=$(grep nameserver /etc/resolv.conf | awk '{print $2}')

# 设置代理端口（例如 v2ray 端口是 10808）
export PROXY_PORT=10808

alias proxy='
    export http_proxy="http://$hostip:$PROXY_PORT"
    export https_proxy="http://$hostip:$PROXY_PORT"
    export all_proxy="socks5://$hostip:$PROXY_PORT"
    echo "Proxy on: $hostip"
'
alias unproxy='
    unset http_proxy
    unset https_proxy
    unset all_proxy
    echo "Proxy off"
'
```

3. 执行 `source ~/.bashrc` 使其生效。
4. 之后只需在终端输入 `proxy` 即可开启代理，输入 `unproxy` 关闭。

# 其它

在 WSL 2 架构下，Ubuntu 并不是以文件夹的形式直接散落在 Windows 磁盘中，而是被封装在一个虚拟磁盘文件（.vhdx）里。默认情况下，Ubuntu 的虚拟磁盘文件位于 Windows 用户目录下：

```
C:\Users\用户名\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu...[一串随机字符]\LocalState\ext4.vhdx
```

`ext4.vhdx`：这个文件就是整个 Ubuntu 的“硬盘”。所有的 Linux 文件、安装的软件、数据库数据都存在这个大文件里。