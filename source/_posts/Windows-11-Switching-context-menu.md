---
title: 切换 Windows 11 右键菜单风格
date: 2021-11-07 09:33:02
tags: Windows
categories:
---

更新到 Windows 11 之后，整体界面焕然一新，虽然推送的是正式版，实则有些东西完全就是半成品，比如右键菜单的功能就过于简陋，所以必须切换回原来的样子。

<!--more-->

1. 以管理员身份打开 Windows 终端。

2. 输入以下 **换回经典** 或 *恢复回 Win11* 的命令，回车运行。

    - 换回原来的样子

        ```
        reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
        ```

    - 回到如今的风格

        ```
        reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
        ```

3. 打开 Windows 资源管理器，然后打开 [任务管理器](https://baike.baidu.com/item/windows%E4%BB%BB%E5%8A%A1%E7%AE%A1%E7%90%86%E5%99%A8/7857349#1_1) ，右键选择 Windows 资源管理器，点击 **重新启动**。

4. 搞定。