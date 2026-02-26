---
title: 修复 NVIDIA GPU 活动面板模糊的问题
tags: Windows
abbrlink: dc62cba0
date: 2022-01-14 20:40:24
categories:
---

NVIDIA GPU 活动面板显示模糊的问题确实是让人头疼 😑。

虽然也有一个凑合的方法——每次开机后再注销一次它就会显示清晰，但每次都注销也太过麻烦 😓。

<!--more-->

长久以来的寻找解决办法，终于 🤦‍

先看一下模糊的样子 👇

<div style="width: 32rem;">
{% asset_img vague.png 'NVIDIA GPU 活动面板模糊的样子' %}
</div>

现在进入这个软件的设置，可以通过资源管理器打开，右键点击属性即可 👇

<div style="width: 32rem;">
{% asset_img step-1.png 步骤-1 %}
</div>

然后 👇，更改 **所有用户** 的 DPI 设置

{% asset_img step-2.png 步骤-2 %}

以后再开机：

<div style="width: 32rem;">
{% asset_img clear.png %}
</div>

这个方法应该也适用于其它软件模糊的情况。😀
