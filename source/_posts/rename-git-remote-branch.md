---
title: Git 重命名远端分支
date: 2023-12-23 16:34:24
tags:
categories:
---

要修改 Git 远程仓库中的分支名称，可以按以下步骤操作：

<!--more-->

1. 如果不在要重命名的分支上，那先切换到该分支

```
git checkout <old-branch-name>
```

2. 重命名本地分支，使用以下命令将本地分支重命名

```
git branch -m <new-branch-name>
```

3. 删除远程仓库中的旧分支（注意冒号）

```
git push origin :<old-branch-name>
```

4. 最后将重命名后的本地分支推送到远端

```
git push origin <new-branch-name>
```