---
title: 在服务器(CentOS)上搭建Git
author: kinglyq
tags:
- Centos7
- Git
date: 2019-06-30 18:20:00
---
> 假装已经安装好Git，建好了组和用户...

# 一 搭建git代码仓库

## (一) 新建git仓库
(仓库位置自己随用户自己决定，例/home/git/test.git)

1. 在/home/git目录下新建 项目名称test.git 文件夹

2. cd /home/git/test.git 进入文件夹。

<!--more-->

~~git init --bare 创建裸库(这里需要注意--bare参数，表示是要生成一个"干净"的仓库)~~

3. 修改权限
```
# chown -R liyuqing:git gittest // liyuqing:用户名    git:组名
# chmod -R 775 gittest
# chmod g+s -R gittest
# sudo chown -R liyuqing:git gittest
```
## (二) 创建证书登录
添加证书之前，还要做这么一步：
Git服务器打开RSA认证 。在Git服务器上首先需要将/etc/ssh/sshd_config中的RSA认证打开，即将sshd_config文件中下面几个的注释解开：

1.RSAAuthentication yes

2.PubkeyAuthentication yes

3.AuthorizedKeysFile .ssh/authorized_keys

**保存后，systemctl restart sshd 生效**

## (三)  配置ssh公钥（无需密码更新代码库）

### 1. 生成 SSH 公钥

- 每个需要使用git仓库的软件开发者，需要在使用git代码库的电脑上面生成一个ssh公钥，具体步骤：
	1. 进入自己的~/.ssh目录(win系统在用户文件夹下：C:\Users\Administrator\.ssh)，查看有没有用 文件名 和 文件名.pub 来命名的一对文件，这个 文件名 通常是 id_dsa 或者 id_rsa。

	2. *.pub 文件是公钥，另一个文件是密钥。假如没有这些文件（或者干脆连 .ssh 目录都没有），在linux下，你可以用 ssh-keygen 的程序来建立它们，该程序在 Linux/Mac 系统由 SSH 包提供； 在 Windows 上则包含在 MSysGit 包里，git安装目录中，bin路径下ssh-keygen.exe。

	运行后，它先要求你确认保存公钥的位置（.ssh/id_rsa），然后它会让你重复一个密码两次，如果不想在使用公钥的时候输入密码，可以留空。

	3. 复制本机的*.pub中的内容添加至git仓库所在服务器的git用户文件夹下的/home/git/.ssh/authorized_keys文件中 可使用命令# $ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys，将公钥内容追加至授权文件中。
	
	4. 如果 ~/.ssh/authorized_keys 不存在，你可以直接将id_rsa.pub 文件复制过去并重命名为authorized_keys即可

## (四)  访问
使用正确的地址

例如：我在 /usr下建立了名为gittest文件夹并将其作为一个仓库，那么我访问的地址就应该是：
```
用户名@服务器ip:/usr/gittest
```

# 二 使用过程中出现的问题

## (一) git push的问题

###  1. 报错remote: error: refusing to update checked out branch... ：
```
remote: error: refusing to update checked out branch: refs/heads/master
remote: error: By default, updating the current branch in a non-bare repository
remote: error: is denied, because it will make the index and work tree inconsistent
remote: error: with what you pushed, and will require 'git reset --hard' to match
remote: error: the work tree to HEAD.
remote: error:
remote: error: You can set 'receive.denyCurrentBranch' configuration variable to
remote: error: 'ignore' or 'warn' in the remote repository to allow pushing into
remote: error: its current branch; however, this is not recommended unless you
remote: error: arranged to update its work tree to match what you pushed in some
remote: error: other way.
remote: error:
remote: error: To squelch this message and still keep the default behaviour, set
remote: error: 'receive.denyCurrentBranch' configuration variable to 'refuse'.
To 47.100.165.17:/usr/hexo/myblog/source
 ! [remote rejected] master -> master (branch is currently checked out)
```

- 这是因为git默认是拒绝push操作的，我们在.git/config里面添加如下配置项即可：
```
 [receive]
    denyCurrentBranch = ignore
```
添加完成之后执行代码` git config receive.denyCurrentBranch ignore`

### 2. 报错remote: error: insufficient permission... :
```
remote: error: insufficient permission for adding an object to repository database ./objects
```

- 没有权限的问题

~~这是当我们初始化一个远程仓库的时候，使用git  --bare  init即可了，而不是使用git  init，这样那么该远程仓库的目录下，也包含work  tree，~~当本地仓库向远程仓库push时，如果远程仓库正在push的分支上时，那么push后的结果不会反映在work  tree上，也就是在远程仓库的目录下对应的文件还是之前的内容，必须使用git  reset  --hard才能看到push之后的内容。

## (二) git pull的问题

git pull 失败 ,提示： `fatal: refusing to merge unrelated histories`

其实这个问题是因为 两个 根本不相干的 git 库， 一个是本地库， 一个是远端库， 然后本地要去推送到远端， 远端觉得这个本地库跟自己不相干， 所以告知无法合并。

使用这个强制的方法： `git pull origin master --allow-unrelated-histories`

# (三) 关于push成功服务器上的内容没有改变

- 在远程创库执行以下命令，才可以看到更新的内容。
```
git config --unset core.bare 首次执行
git reset --hard
```
~~git config --bool core.bare true~~