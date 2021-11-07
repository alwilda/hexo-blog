---
title: 切换 Windows 11 右键菜单风格
date: 2021-11-07 09:33:02
tags:
categories:
---

虽然右键菜单统一风格，但功能过于简陋，所以必须切换回原来的样子。

<!--more-->

1. 以管理员身份打开 Windows 终端。

2. 输入 **切换回经典** 或 *恢复回 Win11* 的命令，回车运行。

    - 切换回经典右键菜单

        ```
        reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
        ```

    - 恢复回 Win11 右键菜单

        ```
        reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
        ```

3. 打开 Windows 资源管理器，然后打开 Windows资源管理器，右键选择 Windows 资源管理器，点击 **重新启动**。

4. 搞定。