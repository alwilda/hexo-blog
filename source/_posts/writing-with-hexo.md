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

## Link

在文章中插入链接，并自动给外部链接添加 `target="_blank"` 属性。

```
{% link text url [external] [title] %}
```

# 资源的引用

> 资源（Asset）代表 `source` 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的 Hexo 项目中只有少量图片，那最简单的方法就是将它们放在 `source/images` 文件夹中。然后通过类似于 `![](/images/image.jpg)` 的方法访问它们。

将 `config.yml` 文件中的 `post_asset_folder` 选项设为 `true` 来打开，这样 Hexo 将会在你每一次通过` hexo new [layout] <title>` 命令创建新文章时自动创建一个与文章同名的文件夹，当然也可以手动创建。

{% codeblock _config.yml lang:yml %}
post_asset_folder: true
{% endcodeblock %}

通过常规的 `markdown` 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。使用以下 `Hexo` 标签来加载资源：

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

例如：`{% asset_img Pikachu.jpg Pikachu %}`

{% asset_img Pikachu.jpg Pikachu %}
