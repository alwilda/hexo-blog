---
title: VSCode 在代码片段中没有提示
date: 2021-05-31 22:34:00
tags: Visual Studio Code
categories:
---

默认情况下，在代码片段中（处于光标聚焦状态）是没有提示的。比如:

<!--more-->

<video width='100%' src="no.mp4" controls></video>

要想在这种情况下有代码提示的话，就得将 `Snippets Prevent Quick Suggestions` 关闭，如下：

{% asset_img suggestions.jpg Prevent-Quick-Suggestions %}

这样的话，在使用的代码片段时，也会有提示。

<video width='100%' src="yes.mp4" controls></video>
