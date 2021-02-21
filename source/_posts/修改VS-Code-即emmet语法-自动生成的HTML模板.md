---
title: 修改VS Code(即emmet语法)自动生成的HTML模板
author: kinglyq
tags:
- vscode
date: 2019-04-27 20:55:38
---
# 修改VS Code(即emmet语法)自动生成的HTML5模板

- 在对emmet配置文件修改前，请务必备份，以防万一。修改emmet配件文件需要关闭VSCode并重新打开方可生效。
## 将H5模板的lang属性值修改成zh-CN/zh-cmn-Hans

1. 找到下面的文件
```
{VSC安装路径}\resources\app\extensions\emmet\node_modules\vscode-emmet-helper\out\expand\expand-full.js
```
<!--more-->

2. 使用notepad或VSC打开它，搜索defaultVariables，在第1个搜索结果中，即可看到关于lang: 'en'的描述，将其中的en替换成zh-cmn-Hans并保存即可。
```js
defaultVariables = { lang: 'en', locale: 'en-US', charset: 'UTF-8' }。
```

## 修改H5模板生成时光标的初始位置

1. 默认情况下，使用！感叹号生成H5模板时，光标默认是选中device-width文本状态，需要3-4个Tab键才能将光标移入body中。
打开xpand-full.js，搜索关键字device-width即可找到如下代码：
```json
"meta:vp": "meta[name=viewport content='width=${1:device-width}, initial-scale=${2:1.0}']",
"meta:edge": "meta:compat[content='${1:ie=edge}']",
```

2. 上面$大括号中的``1:``， ``2:``便是锁定光标的顺序，所以只要删除1: ,2:就行了，但是这样在生成html是她的属性值就变成了${device-width}、${ie=edge}，所以干脆把$和大括号也删掉就好了。

2. VSCode下emmet生成H5模板的简单总结

> expand-full.js文件是emmet在VSCode的全局配件文件。再提醒一次，修改之前请务必备份之，以防不测。

- 英文状态下的!(感叹号)可触发emmet的H5模板。
使用VSC打开expand-full.js文件，定位于5100行。大概有3行代码(逗号分隔)，如下
```json
"!!!": "{<!DOCTYPE html>}", 
"doc": "html[lang=${lang}]>(head>meta[charset=${charset}]+meta:vp+meta:edge+title{${1:Document}})+body", 
"!|html:5": "!!!+doc",
```
第1行的代码的意思大概就是使用3个!即可自动补全<!DOCTYPE html> 
第3行代码的意思是键1个!即可调第1行的补全功能及第2行的补全功能。
重点是第2行代码，${lang}的意思应该是寻找关于lang的变量，我估计直接将常量lang="zh-CN"写死在此处是可行的。${charset}同理可证。
meta:vp将会调用4986行处的代码块，这个块里使用**1:及2:依次控制着2个光标选中状态**，建议清除1:和2:和包裹它们的$及对应的{}。meta:edge同理可证。
title{${1:Document}}，其中title即为H5模板的页面标题，$应该是类似于变量的引用，1:还是意味着初始时光标在标题行的第1次选中Document文本状态，后者也就是模板页面的标题，完全可以修改成自己想要字符。

- 完成修改后，H5模板初始时，光标是<body></body>之间，减少了不必要的干扰，lang的属性值是zh-cmn-Hans，减少了某些浏览器集成语言检测的干扰，还可以将缺省的标题修改成自己的个性文字。

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge,chrome=1">
    <title>Document</title>
</head>
<body>
    
</body>
</html>

charset="UTF-8"的修改应该是在{VSCode安装路径}\resources\app\extensions\html\snippets\html.snippets.json文件中进行。
```