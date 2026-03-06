---
title: Windows 终端集成 Git Bash
abbrlink: 36f041dd
date: 2026-03-06 20:32:11
tags:
  - Windows
  - Git
categories:
---

# 确认 Git Bash 路径

在开始之前，请确保你已经安装了 Git for Windows。默认的安装路径通常是：

* `C:\Program Files\Git\bin\bash.exe`

<!--more-->

# 在 Windows Terminal 中添加配置

1. 打开 Windows Terminal。
2. 按下 `Ctrl + ,`（逗号）或者点击标题栏的下拉箭头，选择 **“设置”**。
3. 在左侧边栏最下方，点击 **“打开 JSON 文件”**（如果你更喜欢图形界面，也可以在“配置文件”里点击“添加新配置文件”）。

## 使用图形界面操作：

* 点击 **“+ 添加新配置文件”**。
* 点击 **“新建空配置文件”**。
* **名称**：填入 `Git Bash`。
* **命令行**：填入上述的路径（例如 `"C:\Program Files\Git\bin\bash.exe" --login -i`）。
* **图标**：可以填入 `C:\Program Files\Git\mingw64\share\git\git-for-windows.ico`。

## 使用 JSON 文件

在 `profiles` -> `list` 数组中，添加以下代码块：

```json
{
    "guid": "{00000000-0000-0000-BA54-000000000000}", // 只要唯一即可
    "name": "Git Bash",
    "commandline": "C:\\Program Files\\Git\\bin\\bash.exe --login -i",
    "icon": "C:\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico",
    "startingDirectory": "%USERPROFILE%",
    "hidden": false
}

```

{% note info no-icon 为什么建议加上 `--login -i`？ %}
* `--login`：确保 Bash 会读取你的配置文件（如 `.bashrc` 或 `.bash_profile`），这样你的别名（alias）和环境变量才会生效。
* `-i`：表示交互模式。
{% endnote %}

如果习惯使用 Git Bash，可以在设置里的 **“启动”** 选项中，将 **“默认配置文件”** 改为 Git Bash。