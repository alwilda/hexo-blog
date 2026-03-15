---
title: Qwen3.5-9B 的 Modelfile
abbrlink: 50b33d69
date: 2026-03-13 21:03:07
tags:
categories:
---

对话时模型出现一直输出不会停止或者自动补充用户提出的问题（比如只问了一句你好，模型以为没有问完，主动补全问题），由于推理时的停止符（Stop Tokens）没有正确触发，或者提示词模板（Prompt Template）出现了偏差，通过一些参数进行调整：

<!--more-->

```dockerfile
FROM "***\Qwen3.5-9B-Q4_K_M.gguf"

# 设置推理参数
PARAMETER temperature 0.7
PARAMETER top_p 0.8
PARAMETER top_k 40
PARAMETER repeat_penalty 1.1

# 核心设置：定义停止符 (Stop Tokens)
PARAMETER stop "<|im_start|>"
PARAMETER stop "<|im_end|>"
PARAMETER stop "<|user|>"
PARAMETER stop "<|assistant|>"

# 定义对话模板 (ChatML 格式)
TEMPLATE """{{ if .System }}<|im_start|>system
{{ .System }}<|im_end|>
{{ end }}{{ if .Prompt }}<|im_start|>user
{{ .Prompt }}<|im_end|>
{{ end }}<|im_start|>assistant
{{ .Response }}<|im_end|>
"""

SYSTEM """你是一个严谨、高效且友好的 AI 助手。
你的任务是准确回答用户的问题，并在回答完毕后立即停止输出。
严禁模拟用户提问或进行无意义的自问自答。
如果问题已经解决，请直接结束对话。"""
```