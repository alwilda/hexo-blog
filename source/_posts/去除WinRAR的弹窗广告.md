---
title: 去除WinRAR的弹窗广告
author: kinglyq
date: 2019-04-04 21:01:29
tags: []
---
- 电脑桌面新建一个txt文件，重命名为“rarreg.key”
- 将.key文件用记事本方式打开，将一下的内容复制粘贴到文本中并保存
<!--more-->
```
	RAR registration data
	Federal Agency for Education
	1000000 PC usage license
	UID=b621cca9a84bc5deffbf
	6412612250ffbf533df6db2dfe8ccc3aae5362c06d54762105357d
	5e3b1489e751c76bf6e0640001014be50a52303fed29664b074145
	7e567d04159ad8defc3fb6edf32831fd1966f72c21c0c53c02fbbb
	2f91cfca671d9c482b11b8ac3281cb21378e85606494da349941fa
	e9ee328f12dc73e90b6356b921fbfb8522d6562a6a4b97e8ef6c9f
	fb866be1e3826b5aa126a4d2bfe9336ad63003fc0e71c307fc2c60
	64416495d4c55a0cc82d402110498da970812063934815d81470829275
```


1. 将该文件复制粘贴到winrar压缩软件安装路径下，替换原文件 (如果系统提示存在同名文件的话)

2. 下载resource hacker，安装版或者绿色版的都行，下载安装完之后先关闭winrar

	- 下载链接：https://pan.baidu.com/s/1F4EeXwxCoYGlvXXjxDU7Cw 
	- 提取码：c00x 

3. 打开resource hacker，点左上角的“文件”，选择winrar安装目录下的winrar.exe，双击打开后在左边找到“字符串表”——> 80: 

4. 按键盘上的delete删除右边字符串里面“1272”最长的一行（不一定是1272，但就是各种符号组合最长的那一串），**点击上面绿色的三角编译脚本**，然后左上角的“文件”——“另存为”，
将反编译好的winrar.exe文件保存在电脑的任意位置 (方便你找到的位置就可以，但不能直接保存在winrar安装目录下)

5. 把刚才保存的.exe文件复制或剪切到winrar的安装目录下，替换原文件就OK了~