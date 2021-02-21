---
title: Hexo底部添加备案信息
author: kinglyq
tags:
- Hexo
categories: []
date: 2019-04-03 22:46:00
---
在所使用主题文件夹下的 /layout/_partial 编辑 footer.swig 在如下位置添加：
<!--more-->
![位置](beianweizhi.png)

根据自己的备案号进行修改
```
<span>
  </br>
  {{ __('豫ICP备') }} -
  <a href="http://www.miitbeian.gov.cn/">18035862号-1</a>
  </a>
</span>
```
保存，hexo clean hexo g ,效果如下：

![效果](xiaoguo.png)