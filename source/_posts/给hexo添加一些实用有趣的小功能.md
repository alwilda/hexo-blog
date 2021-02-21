---
title: 给hexo添加一些实用有趣的小功能
author: kinglyq
tags:
- Hexo
- NexT
categories: []
date: 2019-02-16 11:20:00
---
注意：以下功能是在NexT主题上实现的，有些功能是通用的，有些可能与其他主题有些出入。
# 添加网站网页访问浏览计数器
- 这里使用不蒜子网页计数器
- 进入你使用的主题的文件夹里，打开layout文件夹里的_layout.swig（不要使用记事本，找一个能选择编码格式的文本编辑器，这里使用{% link Notepad++ https://notepad-plus.en.softonic.com/ Notepad++官网下载 %}
）,加入以下代码

<!--more-->

```
<script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
</br>
本站总访问量 <span id="busuanzi_value_site_pv"></span> 次&nbsp&nbsp&nbsp
本站访客数<span id="busuanzi_value_site_uv"></span>人次
```
 ![不蒜子计数器](bszjsq1.jpg)

 - 最后，注意一下 /layout/_third-party/analytics 里的 **busuanzi-counter.swig **文件，看看链接对不对。 

```
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

 {% asset_img bsz.jpg %}

 # 添加点击页面出现的红心
 - 进入你使用的主题的文件夹里，在 **source/js/src** 里创建一js文件，就命名为love.js(名字随意)吧。写入：


 ```
 !function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
 ```
 - 打开layout文件夹里的_layout.swig,&lt;body&gt;标签最后添加：


 ```
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
 ```
# 侧边栏社交小图标
- 打开主题配置文件_config.yml，搜索social:, || 之后是在图标库中对应的图标。注意空格。

# 主页文章加阴影
- 打开\themes\next\source\css\_custom\custom.styl,向里面加入：

```
// 主页文章添加阴影效果
.post {
margin-top: 60px;
margin-bottom: 60px;
padding: 25px;
-webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
-moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
}
```

# 侧边栏添加音乐播放
## 使用网易云音乐的外链
- 访问 {% link 网易云音乐 https://music.163.com/ 网易云音乐 %}，找到想要使用的歌曲然后**生成外链播放器**。
- 将代码放到所用主题文件夹/layout/_macro下的sidebar.swig文件里。
 ![音乐代码位置](music.jpg)
- 网易云音乐的外链确实很方便，但是有一个问题就是**版权！**所以好多歌曲不能生成外链。So
## 使用本地音乐
- **暂时**~~不想写了，不过你可以访问上图框框里的地址，相信会有收获的。~~


# 添加Fork me on Github
- 在http://tholman.com/github-corners/ 或者 https://github.com/blog/273-github-ribbons 选择合适的样式复制代码。
- 到themes/next/layout/_layout.swig，将代码放到&lt;div class="headband"&gt;</div>下面： 
{% asset_img fork.jpg %}
注意划线部分代码，如果 github 标示不能正常显示在页面表层则添加

```
z-index: 100; //z-index 属性设置元素的堆叠顺序。拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。
```
- 然后可以通过定位进行微调。

# 增加打赏功能

**这个是在NexT主题上添加的**

- 将支付宝、微信的收钱码图片上传到hexo的** source/images** 文件夹里。（额，最好用修图工具将两个图片的分辨率调一致，这样在页面上比较好看一点）
- 在 **主题**  配置文件_config.yml里添加如下内容：

```
#打赏 
reward_comment: 喜欢文章就打赏一包辣条吧！
alipay: /images/sqz.jpg
wechatpay: /images/sqw.png
```
到这里就完成了，不过鼠标放到收钱码上文字会闪动，想要取消就：

- 修改next/source/css/_common/components/post/post-reward.styl ，注释掉下面的代码

```
/* 
#wechat:hover p{

animation: roll 0.1s infinite linear;
-webkit-animation: roll 0.1s infinite linear;
-moz-animation: roll 0.1s infinite linear;
}

#alipay:hover p{

animation: roll 0.1s infinite linear;
-webkit-animation: roll 0.1s infinite linear;
-moz-animation: roll 0.1s infinite linear;
}
*/
```