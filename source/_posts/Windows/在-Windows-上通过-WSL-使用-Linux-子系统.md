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

{% note info%}
在 WSL 2 架构下，Ubuntu 并不是以文件夹的形式直接散落在 Windows 磁盘中，而是被封装在一个虚拟磁盘文件（.vhdx）里。默认情况下，Ubuntu 的虚拟磁盘文件位于 Windows 用户目录下：
```
 C:\Users\用户名\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu...[一串随机字符]\LocalState\ext4.vhdx
 ```
 ext4.vhdx 这个文件就是整个 Ubuntu 的“硬盘”，所有的 Linux 文件、安装的软件、数据库数据都存在这个大文件里。
{% endnote %}

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
- 进入 Linux 在命令行输入：
```bash
wsl
```
- 查看状态（查看已安装的版本和运行状态）：
```bash
wsl -l -v
```
- 关闭 WSL（当需要彻底重启 Linux 或是释放内存时使用）：
```bash
wsl --shutdown
```

# 文件管理

{% tabs apt %}
<!-- tab 从资源管理器访问-->
在搜索或地址栏输入 `\\wsl$` 并打开，即可看到所有已安装的 Linux 发行版（如 Ubuntu），双击进入即可通过拖拽、复制、粘贴来传输文件。

在 WSL 终端中输入 `explorer.exe .`（注意后面有个点），可以直接在当前 Linux 路径下打开 Windows 文件夹窗口。
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

如果是在设置里重置的系统，导致如下错误，那么也执行同样执行一下上面的命令。

```
WSL2: 系统找不到指定的文件。
错误代码: Wsl/Service/CreateInstance/MountDisk/HCS/ERROR_FILE_NOT_FOUND
```

# 使用本地代理

以 v2ray 为例：

1. 在 v2rayN 参数设置里启用 “允许来自局域网的连接”。
2. 获取 Windows 宿主机 IP 并设置环境变量：

```bash
vim ~/.bashrc
```

```bash 
# 获取宿主机 IP
export hostip=$(ip route show | grep -i default | awk '{ print $3}')

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

3. 使配置生效：

```bash
source ~/.bashrc
```

4. 之后只需在终端输入 `proxy` 即可开启代理，输入 `unproxy` 关闭。

# 释放系统空间

>释放占用的空间是一个非常常见的需求，因为 WSL 2 使用的是虚拟硬盘（.vhdx 文件），它的特点是会自动变大，但删除文件后不会自动变小。

在进行压缩前，必须彻底关闭 WSL。打开 Windows PowerShell（管理员身份），运行：

```powershell
wsl --shutdown
```

继续在管理员身份的 PowerShell 中执行以下命令（将下方的路径替换为实际的 ext4.vhdx 路径）：

```powershell
# 1. 启动 diskpart 工具
diskpart

# 2. 选择 WSL 虚拟硬盘文件（路径要加双引号）
select vdisk file="C:\Users\YOUR_USERNAME\AppData\Local\Packages\..."

# 3. 以只读模式附加（部分系统版本需要这一步）
attach vdisk readonly

# 4. 执行压缩
compact vdisk

# 5. 分离硬盘并退出
detach vdisk
exit
```

完成之后，再查看该 `.vhdx` 文件，会发现它的体积明显变小了。