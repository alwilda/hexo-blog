---
title: 在 WSL 中安装 OpenClaw
abbrlink: 7cef2500
date: 2026-03-16 21:24:47
tags:
categories:
---

在 WSL 中安装 OpenClaw 并使用本地 Ollama/LM Studio 中运行的模型。

<!--more-->

通过 WSL2（实例）在 Linux 分发中运行的程序想要知道 Windows 主机的 IP 地址可以使用以下命令获取，以便 Linux 程序可以连接到 Windows 主机服务器程序。[^1]

```bash
ip route show | grep -i default | awk '{ print $3}'
```

假设得到的 IP 地址是：`172.30.98.229`

# 调用 Ollama

确保 Ollama 启动时绑定 0.0.0.0，否则无法在 WSL 中访问。

```
OLLAMA_HOST=0.0.0.0
```

得到 IP 地址后，尝试访问 Windows 主机的 Ollama 服务，如果无法访问，**请检查 Windows 防火墙（入站规则）是否阻止了访问**。

安装 OpenClaw 后直接在配置文件中配置 Ollama 的服务：

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

# 调用 LM Studio

## 应用设置

1. 启动服务并开启“在网络中提供服务”：

<div style="width: 50%">
{% asset_img lm-settings-1.png %}
</div>

2. 配置文件中直接配置 LM Studio 的服务：

{% codeblock  lang:json ~/.openclaw/openclaw.json %}
{
  "models": {
    "providers": {
      "lm-studio": {
        "baseUrl": "http://172.30.98.229:1234/v1",
        "apiKey": "lm-studio",
        "api": "openai-completions",
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

{% note primary no-icon %}
即使没有在 LM Studio 中开启认证，这里的 `"apiKey"` 也不能为空。
{% endnote %}

## 错误处理

如果在对话时报错：

```
The number of tokens to keep from the initial prompt is greater than the context length (n_keep: 15507>= n_ctx: 4096). 
Try to load the model with a larger context length, or provide a shorter input.
```

请在加载模型时调大上下文长度，例如提升到 16384 (16k) 或 32768（32k），具体取决于显存大小。

# OpenClaw 设置

1. 如果配置了 `OPENCLAW_HOME` 环境变量，先执行一下 `openclaw setup`。

# 其它：

- [故障排除 - OpenClaw](https://docs.openclaw.ai/zh-CN/gateway/troubleshooting)
- [OpenClaw 部署常见问题全解 - 博客园](https://www.cnblogs.com/qiniushanghai/p/19706144)

[^1]: [使用 WSL 访问网络应用程序 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/networking)