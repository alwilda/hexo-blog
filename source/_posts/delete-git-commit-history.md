---
title: Git 删除提交记录
date: 2022-04-30 18:30:50
tags: Git
categories:
---

1. 使用 git log 查找到要删除提交记录的上一条提交的 commit-id。

<!--more-->

2. 执行 `git rebase -i <commit-id>`

3. vim 普通模式下，光标移到要删的那一行，执行 `dd` 删除所在行（按 i 进入编辑模式，把需要删除的记录的 `pick` 改为 `drop`，然后按 esc 退出 :wq 保存。

5. 再次查看 git log，可以看到记录已经没有了。