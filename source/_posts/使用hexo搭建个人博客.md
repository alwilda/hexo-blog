---
title: 使用hexo搭建个人博客
author: kinglyq
tags:
- Hexo
categories: []
date: 2019-02-02 14:22:00
---
## 测试
使用hexo的第一篇文章
hexo-admin

<!--more-->

{% blockquote %}
引用内容
{% endblockquote %}

{% codeblock %}
代码块
alert('Hello World!');
{% endcodeblock %}

## 图片的引用
### source/images引用
{% blockquote %}
	资源（Asset）代表 source 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的Hexo项目中只有少量图片，那最简单的方法就是将它们放在 source/images 文件夹中。然后通过类似于 ** - !&#91;&#93;&#40;images/img.jpg&#41; ** 的方法访问它们。
{% endblockquote %}
### 相对路径的引用
   1. 把主页配置文件_config.yml 里的post_asset_folder:这个选项设置为true。
   2. 在你的hexo目录下执行这样一句话npm install hexo-asset-image --save，这是下载安装一个可以上传本地图片的插件。
   3. 等待一小段时间后，再运行hexo n "xxxx"来生成md博文时，/source/_posts文件夹内除了xxxx.md文件还有一个同名的文件夹 （当然也可以自己手动建）
   4. 最后在xxxx.md中想引入图片时，先把图片复制到xxxx这个文件夹中，然后只需要在xxxx.md中按照markdown的格式引入图片：!&#91;你想输入的替代文字&#93;(xxxx/图片名.jpg)。
   5. 注意： xxxx是这个md文件的名字，也是同名文件夹的名字。只需要有文件夹名字即可，不需要有什么绝对路径。你想引入的图片就只需要放入xxxx这个文件夹内就好了，很像引用相对路径。
   6. 最后检查一下，hexo g生成页面后，进入public\2017\02\26\index.html文件中查看相关字段，可以发现，html标签内的语句是&lt;img src="2017/02/26/xxxx/图片名.jpg"&gt;，而不是<img src="xxxx/图片名.jpg>。这很重要，关乎你的网页是否可以真正加载你想插入的图片。

*使用 MarkDown 语法添加图片*

- !&#91;lbj&#93;&#40;使用hexo搭建个人博客/LBJ001.jpg&#41;
![lbj](LBJ001.jpg)

> 2019年7月6日 21:41:01补充
> ps:之前在服务器上使用MarkDown一直是（文章文件夹名/图片名.png）这种标准的格式。图片链接是这样的: localhost:4000/2019/02/02/使用hexo搭建个人博客/LBJ001.jpg
> 但是我在windows使用hexo链接却变成了localhost:4000/2019/02/02/使用hexo搭建个人博客/使用hexo搭建个人博客/LBJ001.jpg
>
> 所以只能是去掉文章文件夹名直接写图片名。
>
> 也就是!&#91;lbj&#93;&#40;使用hexo搭建个人博客/LBJ001.jpg）变成   !&#91;lbj&#93;&#40;LBJ001.jpg)
>
> 在编辑器写上图片所在文件名才是对的，这样才能读取，但是hexo对于md语法给自动添加了，这实在是画蛇添足。

![路径的差异](路径的差异.jpg)

> 可以看出一个变成了相对路径，一个变成了绝对路径。

使用 hexo 语法添加图片*

- &#123;%&nbsp;asset_img LBJ001.jpg&nbsp;%&#125;
{% asset_img LBJ001.jpg %}