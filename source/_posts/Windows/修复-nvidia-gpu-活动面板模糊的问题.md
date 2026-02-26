---
title: 修复 NVIDIA GPU 活动面板模糊的问题
tags: Windows
abbrlink: dc62cba0
date: 2022-01-14 20:40:24
categories:
---

长久以来伴随着打开这玩意儿就显示模糊的问题的确是~~让人荡气回肠，精彩纷呈，读来~~令人茶饭不思，一病不起 😑。。。

虽然也有一个相当凑合的方法——每次开机后再注销一次它就会显示清晰。但这也并不是长久之计，每次都注销也太烦了 😓。

<!--more-->

长久以来的寻找解决办法，终于 🤦‍

首先：回顾一下这模糊的样子（也许以后会怀念的 🧐） 👇

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

最后：

> 猜想：这个方法应该也适用于其它软件模糊的情况。(⊙﹏⊙) 可能吧 ε=ε=ε=┏(゜ロ゜;)┛ 😊
