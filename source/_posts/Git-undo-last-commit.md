---
title: Git 撤销上次的提交
date: 2022-04-30 18:32:03
tags:
categories: Git
---

这条命令就能撤回刚刚的提交。
```
git reset HEAD^
```

更多的参数：
<!--more-->
```
git reset [--soft | --mixed | --hard] [-q] [<commit>]
```

`--mixed`
不删除工作空间改动代码，撤销 commit，并且撤销git add . 操作
这个为默认参数，`git reset --mixed HEAD^` 和 `git reset HEAD^` 效果是一样的。

`--soft`
不删除工作空间改动代码，撤销 commit，不撤销 git add .

`--hard`
删除工作空间改动代码，撤销 commit，撤销 git add .
{% note warning %}
注意！完成这个操作后，会删除工作空间代码！恢复到上一次的 commit 状态，慎重使用！
{% endnote %}

