---
title: Qwen3.5-9B 的 Modelfile
abbrlink: 50b33d69
date: 2026-03-13 21:03:07
tags:
categories:
---

对话时模型出现一直输出不会停止或者自动补充用户提出的问题（比如只问了一句你好，模型以为没有问完，主动补全问题），由于推理时的停止符（Stop Tokens）没有正确触发，或者提示词模板（Prompt Template）出现了偏差，通过一些参数进行调整：

<!--more-->

GGUF 格式下载地址：[Qwen3.5-9B-GGUF · 模型库](https://modelscope.cn/models/unsloth/Qwen3.5-9B-GGUF)。

```dockerfile
# 替换为实际路径
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

# 定义对话模板
TEMPLATE """{{- if .Messages }}
{{- if or .System .Tools }}<|im_start|>system
{{- if .System }}
{{ .System }}
{{- end }}
{{- if .Tools }}

# Tools

You may call one or more functions to assist with the user query.

You are provided with function signatures within <tools></tools> XML tags:
<tools>
{{- range .Tools }}
{"type": "function", "function": {{ .Function }}}
{{- end }}
</tools>

For each function call, return a json object with function name and arguments within <tool_call></tool_call> XML tags:
<tool_call>
{"name": "<tool_name>", "arguments": <args-json-object>}
</tool_call><|im_end|>
{{- end }}
{{- end }}
{{- range $i, $_ := .Messages }}
{{- $last := eq (len (slice $.Messages $i)) 1 -}}
{{- if eq .Role "user" }}<|im_start|>user
{{ .Content }}<|im_end|>
{{- else if eq .Role "assistant" }}<|im_start|>assistant
{{- if .Content }}
{{ .Content }}
{{- else if .ToolCalls }}<tool_call>
{{ range .ToolCalls }}{"name": "{{ .Function.Name }}", "arguments": {{ .Function.Arguments }}}
{{ end }}</tool_call>
{{- end }}{{ if not $last }}<|im_end|>
{{- end }}
{{- else if eq .Role "tool" }}<|im_start|>user
<tool_response>
{{ .Content }}
</tool_response><|im_end|>
{{- end }}
{{- if and $last (ne .Role "assistant") }}<|im_start|>assistant
{{- end }}
{{- end }}
{{- else }}
{{- if .System }}<|im_start|>system
{{ .System }}<|im_end|>
{{- end }}
{{- if .Prompt }}<|im_start|>user
{{ .Prompt }}<|im_end|>
{{- end }}<|im_start|>assistant
{{ end }}{{ .Response }}{{ if .Response }}<|im_end|>{{ end }}
"""

SYSTEM """你是一个严谨、高效且友好的 AI 助手。
你的任务是准确回答用户的问题，并在回答完毕后立即停止输出。
严禁模拟用户提问或进行无意义的自问自答。
如果问题已经解决，请直接结束对话。"""
```

创建模型的命令：

```bash
ollama create qwen3.5-9b -f Modelfile
```

[LM Studio with AMD RyzenAI](https://lmstudio.ai/ryzenai)