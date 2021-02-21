---
title: Git的一些操作
author: kinglyq
tags:
- Git
date: 2019-05-12 17:42:19
---
# 删除Git本地仓库

1. 找到本地仓库的目录，在git的命令窗口打开
2. $ rm -rf  .git &nbsp;&nbsp;&nbsp;&nbsp; 删除 .git 文件夹

<!--more-->

# 重命名文件
```
git mv file_name new_file_name
git commit -m'添加注释' 
```


# 删除GitHub上的某个文件夹

1. 找个文件夹把项目从github上克隆下来
2. 把项目在Git的窗口里打开
3. 输入命令

```
git rm -r --cached 文件夹名 
```

4.  提交并写上日志

```
git commit -m '删除了xxx'  
```

5. 最后上传到 github OK!

```
git push // 上传
```

# 拉取同步
```
git pull
```