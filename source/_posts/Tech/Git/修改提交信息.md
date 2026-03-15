---
title: Git 修改提交信息
tags: Git
abbrlink: d511bc6e
date: 2022-04-30 18:33:26
categories:
---
 
1. 输入如下命令进入变基， head 后的数字表示显示最近多少次的提交信息

```bash
git rebase -i HEAD~2 
```

<!--more-->

2. 输入 **`i`** 进入编辑模式

3. 选择需要修改的那一行提交信息，将其前面的 *pick* 改为 *edit*

4. 输入 **`:wq`** 保存退出

5. 修改提交记录

```bash
git commit --amend -m '新的提交信息'
``` 

6. 退出 rebase 模式

```bash
git rebase --continue
``` 

> `git rebase --abort`
