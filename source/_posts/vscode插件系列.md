---
title: vscode插件系列
author: kinglyq
tags:
- vscode
categories: []
date: 2019-07-07 14:32:35
---
# 必备插件

- 已经安装的
	1. Auto Rename Tag，非常实用！要修改标签名称的时候自动修改结束标签，节省一半时间，提升效率，非常棒！
	
	2. Chinese (Simplified) Language Pack for Visual Studio Code 适用于 VS Code 的中文（简体）语言包   <!--more-->
3. ESLint	
	4. HTML CSS Support，在编写样式表的时候，自动补全功能大大缩减了编写时间，推荐！ 
	5. HTML Snippets，这款插件包含html标签，非常全，很实用；
	6. vscode-icons，这款必须要推荐，明显提升效率的小插件，在项目文件多类型多的情况下，找到制定文件会大大缩短时间；  
	7. JavaScript Snippet Pack，针对js的插件，包含了js的常用语法关键字，很实用；  
	8. jQuery Code Snippets：juqery提示插件    
	9. open in brower 在浏览器中运行  
	10. Path Intellisense：自动路劲补全，默认不带这个功能的，赶紧装  
	11. Markdown TOC 生成目录
		- 找到文件的Eol可以看到默认行尾字符设置为auto。
	  12. Markdown PDF Markdown生成PDF(在setting.json设置一下chrome的路径)
```
	    "markdown-pdf.executablePath": "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chrome.exe"
```

- 尚未安装的

    1. Class autocomplete for HTML，编写html代码的朋友们对html代码的一大体现就是重复，如果纯用手敲不仅累还会影响项目进度，这款自动补全插件真的很棒；
    2. beautify，这款类似于vscode里格式化代码的功能，不错；
    3. Emoji，很好玩的一款插件，可以在代码中插入emoji了，也许是程序猿的娱乐方式吧；
    4. Can I Use，自动检测所写代码能否在相应容器正常编译执行；
    5. Auto Close Tag，编写html代码的时候，写完开始标签，这款插件会自动补全结束标签，其实上面所说的html自动补全插件一个Tab就搞定了，不过有时也需要这款插件；
    6. Debugger for Chrome：让 vscode 映射 chrome 的 debug功能，静态页面都可以用 vscode 来打断点调试。
    7. Debugger for Firefox，在Firefox浏览器中调试。
    8. Import Cost 引入包大小计算,对于项目打包后体积掌握很有帮助

- 附录
    [vscode插件推荐](https://segmentfault.com/a/1190000006697219 "vscode插件推荐")。

# 修改自动生成html的基本标签

- 路径
```
C:\Users\75536\AppData\Local\Programs\Microsoft VS Code\resources\app\extensions\emmet\node_modules\vscode-emmet-helper\out\expand\expand-full.js
```