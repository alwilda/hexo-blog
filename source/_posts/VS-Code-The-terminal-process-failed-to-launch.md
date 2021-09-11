---
title: VS Code 终端进程启动失败
date: 2021-09-11 14:50:00
tags:
categories:
---

关于 VS Code 打开终端报错——终端进程启动失败： A native exception occurred during launch (Unable to start terminal process: CreateProcess failed) 的解决方案。

<!--more-->

在配置项 `terminal.integrated.shell.windows` 提示已被弃用且配置了也好像无济于事的情况下，我们应该就要按其提示的使用新的配置方式。

-- 图

当输入 `terminal.integrated.profiles.windows`，VS Code 会给出提示并在确定后自动给出默认配置，类似如下的样子：

```json
"terminal.integrated.profiles.windows": {
  "PowerShell": {
    "source": "PowerShell",
    "icon": "terminal-powershell"
  },
  "Command Prompt": {
    "path": [
      "${env:windir}\\Sysnative\\cmd.exe",
      "${env:windir}\\System32\\cmd.exe"
    ],
    "args": [],
    "icon": "terminal-cmd"
  },
  "Git Bash": {
    "source": "Git Bash"
  }
}
```

但是仅仅这样还是不够的，上面只相当于列出一个可用终端类型的列表，你还需要一个配置去指定默认要使用的终端类型，如下：

```json
 "terminal.integrated.defaultProfile.windows": "Git Bash"
 ```

 如此配好之后，便可以正常打开终端了。

另一个问题❓

现在打开终端是没问题了，但是我们通过 VS Code 去运行 npm 脚本时，却还提示

```shell
> Executing task: yarn run start <

终端进程启动失败: A native exception occurred during launch (Unable to start terminal process: CreateProcess failed)。
```

好吧，还需要一个配置（怎么这么多配置？），就是：

```json
// 一个路径，设置后将替代 terminal.integrated.shell.windows，并忽略与自动化相关的终端使用情况(例如任务和调试)的 shellArgs 值。
"terminal.integrated.automationShell.windows": "C:\\WINDOWS\\System32\\cmd.exe"
```

在这个配置中，我试图使用 Git Bash 的路径，但并不能用。