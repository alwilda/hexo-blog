---
title: Centos7安装高版本git
author: kinglyq
tags:
- Centos7
- Git
categories: []
date: 2019-02-11 21:51:00
---
使用命令*** git --version *** 查看系统是否已经安装git,而且多是1.8版本的git（使用 ***yum install -y git*** 安装git也是1.8的版本）,不过这个版本可能有些低，所以需要手动安装较高的的版本。 
<!--more-->
## 步骤
- 使用命令 *** yum remove git *** 移除旧版本。
- 可以访问 {% link mirrors.edge.kernel.org/pub/software/scm/git/ https://mirrors.edge.kernel.org/pub/software/scm/git/ external %} 来查看选择或者下载git的各个版本。

- 安装git的依赖库

```
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-deve
yum install gcc perl-ExtUtils-MakeMaker 
```

- 下载高版本git	
 使用*wget*（一个从网络上自动下载文件的自由工具)，或者直接从上述网站上下载好上传到服务器。

```
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz 
```
- 解压，然后进入解压后的文件夹

```
tar -zxvf git-2.9.5.tar.gz 
```
- 编译安装，配置

```
./configure --prefix=/usr/local/git
 make & make install
```
- 设置环境变量

```
echo "export PATH=$PATH:/usr/local/git/bin">>/etc/bashrc
source /etc/bashrc
git --version
```
- 如果查看版本是1.8的话，你可以卸载了它，然后重新生效下环境变量就可以了。

```
sudo yum remove git
source /etc/bashrc
git --version

```