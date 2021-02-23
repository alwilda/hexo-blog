---
title: 使用Hexo写作
date: 2021-02-21 21:12:56
tags:
---

# Hexo 标签

<!-- more -->

{% blockquote Hexo https://hexo.io/zh-cn/docs/tag-plugins %}
因为使用 Markdown ，所以只列举一些特别的标签
{% endblockquote %}

## 引用块

在文章中插入引言，可包含作者、来源和标题

别号： quote

```
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

## iframe

在文章中插入 iframe。

```
{% iframe url [width] [height] %}
```

## 文章摘要和截断

在文章中使用 `<!-- more -->`，那么 `<!-- more -->` 之前的文字将会被视为摘要。首页中将只出现这部分文字，同时这部分文字也会出现在正文之中。

## 代码块

在文章中插入代码。

别名： code

```
{% codeblock [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}
```

1. 普通的代码块

```
{% codeblock %}
alert('Hello World!');
{% endcodeblock %}
```

{% codeblock %}
alert('Hello World!');
{% endcodeblock %}

2. 指定语言

```
{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}
```

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

3. 附加说明和网址

```
{% codeblock lang:js Array.map https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map Array.prototype.map() - JavaScript | MDN %}
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
{% endcodeblock %}
```

{% codeblock lang:js Array.map https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map Array.prototype.map() - JavaScript | MDN %}
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x \* 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
{% endcodeblock %}

## 反引号代码块

另一种形式的代码块，不同的是它使用三个反引号来包裹。

````
``` [language] [title] [url] [link text] code snippet ```
````

# Link

在文章中插入链接，并自动给外部链接添加 `target="_blank"` 属性。

```
{% link text url [external] [title] %}
```
