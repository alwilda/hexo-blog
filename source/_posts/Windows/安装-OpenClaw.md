---
title: 在 WSL 中安装 OpenClaw
abbrlink: 7cef2500
date: 2026-03-16 21:24:47
tags:
categories:
---

在 WSL 中安装 OpenClaw 并使用本地 Ollama 中运行的模型。

<!--more-->

确保 Ollama 启动时绑定 0.0.0.0，否则无法在 WSL 中访问。

```
OLLAMA_HOST=0.0.0.0
```

通过 WSL2（实例）在 Linux 分发中运行的程序想要知道 Windows 主机的 IP 地址可以使用以下命令获取，以便 Linux 程序可以连接到 Windows 主机服务器程序。[^1]

```bash
ip route show | grep -i default | awk '{ print $3}'
```

假设得到的 IP 地址是：`172.30.98.229`

得到 IP 地址后，尝试访问 Windows 主机的 Ollama 服务，如果无法访问，**请检查 Windows 防火墙（入站规则）是否阻止了访问**。

安装 OpenClaw 后直接在配置文件中配置 Ollama 的地址：

{% codeblock  lang:json ~/.openclaw/openclaw.json %}
{
  "models": {
    "providers": {
      "ollama": {
        "baseUrl": "http://172.30.98.229:11434",
        "api": "ollama",
        "models": [
          {
            "id": "qwen3.5-9b",
            "name": "qwen3.5-9b"
          }
        ]
      }
    }
  }
}
{% endcodeblock %}

```bash
netstat -ano | findstr :11434
```

[^1]: [使用 WSL 访问网络应用程序 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/networking)