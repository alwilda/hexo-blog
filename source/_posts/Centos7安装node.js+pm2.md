---
title: Centos7安装node.js+pm2
author: kinglyq
tags: []
categories: []
date: 2019-02-15 11:26:00
---
Linux 上安装 Node.js
直接使用已编译好的包
Node 官网已经把 linux 下载版本更改为已编译好的版本了，我们可以直接下载解压后使用：
 wget https://nodejs.org/dist/v10.9.0/node-v10.9.0-linux-x64.tar.xz    // 下载
 tar xf  node-v10.9.0-linux-x64.tar.xz       // 解压
 cd node-v10.9.0-linux-x64/                  // 进入解压目录
 ./bin/node -v                               // 执行node命令 查看版本
v10.9.0

<!--more-->

解压文件的 bin 目录底下包含了 node、npm 等命令，我们可以使用 ln 命令来设置软连接：
ln -s /usr/software/nodejs/bin/npm   /usr/local/bin/ 
ln -s /usr/software/nodejs/bin/node   /usr/local/bin/
Ubuntu 源码安装 Node.js
以下部分我们将介绍在 Ubuntu Linux 下使用源码安装 Node.js 。 其他的 Linux 系统，如 Centos 等类似如下安装步骤。
在 Github 上获取 Node.js 源码：
$ sudo git clone https://github.com/nodejs/node.git
Cloning into 'node'...
修改目录权限：
$ sudo chmod -R 755 node
使用 ./configure 创建编译文件，并按照：
$ cd node
$ sudo ./configure
$ sudo make
$ sudo make install
查看 node 版本：
$ node --version
v0.10.25
Ubuntu apt-get命令安装
命令格式如下：
sudo apt-get install nodejs
sudo apt-get install npm
CentOS 下源码安装 Node.js
1、下载源码，你需要在https://nodejs.org/en/download/下载最新的Nodejs版本，本文以v0.10.24为例:
cd /usr/local/src/
wget http://nodejs.org/dist/v0.10.24/node-v0.10.24.tar.gz
2、解压源码
tar zxvf node-v0.10.24.tar.gz
3、 编译安装
cd node-v0.10.24
./configure --prefix=/usr/local/node/0.10.24
make
make install
4、 配置NODE_HOME，进入profile编辑环境变量
vim /etc/profile
设置 nodejs 环境变量，在 export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL 一行的上面添加如下内容:
#set for nodejs
export NODE_HOME=/usr/local/node/0.10.24
export PATH=$NODE_HOME/bin:$PATH
:wq保存并退出，编译/etc/profile 使配置生效
source /etc/profile
验证是否安装配置成功
node -v
输出 v0.10.24 表示配置成功
npm模块安装路径
/usr/local/node/0.10.24/lib/node_modules/
注：Nodejs 官网提供了编译好的 Linux 二进制包，你也可以下载下来直接应用。

npm install -g pm2

whereis pm2
pm2: /opt/nodejs/bin/pm2

sudo ln -s /opt/nodejs/bin/pm2 /usr/bin/pm2

sudo ln -s /usr/node/node-v10.15.1-linux-x64/bin/pm2 /usr/bin/pm2