---
title: Hexo 文章重命名后的路径访问问题
tags: Hexo
abbrlink: 1511d7f4
date: 2021-03-25 23:56:06
categories:
---

修改了文章文件名的大小写后，发现其部署到 `GitHub` 后并没有变化……

<!--more-->

解决方案：删除 `.deploy_git` 文件夹后重新部署。
