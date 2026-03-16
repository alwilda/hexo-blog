---
title: Ubuntu 笔记
abbrlink: c9014219
date: 2026-03-15 17:58:59
tags:
categories:
---

# 查看系统信息

- 查看版本信息：

```bash
lsb_release -a
```

- 查看详细系统状态（包含内核和架构）：

```bash
hostnamectl
```

<!--more-->

这个命令不仅能看到 Ubuntu 版本，还能看到当前运行的内核版本 (Kernel) 以及硬件架构（如 x86_64）。

# 配置 APT 镜像源

{% tabs apt %}
<!-- tab 24.04 开始使用的新格式-->
>从 24.04 开始，Ubuntu 默认使用 DEB822 格式，配置文件位于 `/etc/apt/sources.list.d/ubuntu.sources`。

1. 备份原配置：

```bash
sudo cp /etc/apt/sources.list.d/ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources.bak
```

2. 快捷修改（以清华源为例）：

```bash
sudo sed -i 's/http:\/\/archive.ubuntu.com/https:\/\/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list.d/ubuntu.sources
sudo sed -i 's/http:\/\/security.ubuntu.com/https:\/\/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list.d/ubuntu.sources
```
<!-- endtab -->

<!-- tab 22.04 及以前的传统配置方式-->
配置文件路径: `/etc/apt/sources.list`

```bash
# 备份
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

# 替换为清华源
sudo sed -i 's|http://archive.ubuntu.com|https://mirrors.tuna.tsinghua.edu.cn|g' /etc/apt/sources.list
sudo sed -i 's|http://security.ubuntu.com|https://mirrors.tuna.tsinghua.edu.cn|g' /etc/apt/sources.list
```
<!-- endtab -->
{% endtabs %}

修改完成后，必须运行以下命令让系统识别新镜像：

```bash
sudo apt update
``` 

如果输出中显示 `Get:1 https://mirrors.tuna.tsinghua.edu.cn/...`，则说明镜像切换成功。

# 修改系统语言为中文

1. 安装中文语言包：

```bash
sudo apt update
sudo apt install language-pack-zh-hans
```

2. 设置系统默认语言：

使用以下命令将语言环境变量写入配置文件：

```bash
sudo localectl set-locale LANG=zh_CN.UTF-8
```

{% note （可选）通过命令行手动选择语言：%}

```bash
sudo dpkg-reconfigure locales
```

在列表中找到 `zh_CN.UTF-8 UTF-8`，按空格选中，然后确定。
{% endnote %}

3. 重启系统：

```bash
sudo reboot
```