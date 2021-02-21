---
title: docker的安装与卸载
author: kinglyq
tags:
categories: []
date: 2019-8-2 20:13:31
---
> **修改为阿里yum源-mirrors.aliyun.com**

# 一 安装docker

1. Docker 要求 CentOS 系统的内核版本高于 3.10,通过 **uname -r** 命令查看你当前的内核版本

2. 使用 root 权限登录 Centos。确保 yum 包更新到最新。
```shell
sudo yum update
```

<!--more-->

3. 卸载旧版本(如果安装过旧版本的话) <a href="#uninstall_docker">查看卸载办法</a>

4. 安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
```shell
sudo yum install -y yum-utils device-mapper-persistent-data lvm2 #yum 配置管理工具
```

5. 设置yum源
```shell
sudo yum-config-manager --add-repo 
https://download.docker.com/linux/centos/docker-ce.repo

或者 清华大学的 Docker 安装源
sudo yum-config-manager --add-repo 
https://mydream.ink/utils/container/docker-ce.repo

报错：
adding repo from: https://mydream.ink/utils/container/docker-ce.repo
  grabbing file https://mydream.ink/utils/container/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
  Could not fetch/save url https://mydream.ink/utils/container/docker-ce.repo to file /etc/yum.repos.d/docker-ce.repo: [Errno 14] curl #60 - "Peer's Certificate has expired."

出现该问题一般是由于本地时间不正确（经常挂起的虚拟机很容易出现），使用date命令核对一下时间即可，若确认是这个问题，则：
sudo ntpdate pool.ntp.org # ntpdate 可使用 yum install ntpdate 进行安装
```

6. 安装最新版的 Docker CE
```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

7. 镜像加速 新建或修改 **/etc/docker/daemon.json** ，加入：
```json
{
    "registry-mirrors": [
        "https://dockerhub.azk8s.cn",
        "https://reg-mirror.qiniu.com"
    ]
} 
```

- 一定要确保格式没有问题，否则 docker 无法启动，修改完成后执行以下命令：
```shell
sudo systemctl daemon-reload
```

7. 启动并加入开机启动
```shell
sudo systemctl start docker # 启动
sudo systemctl enable docker # 开机启动
```

8. 验证安装是否成功(有client和service两部分表示docker安装启动都成功了)
```shell
docker version
```

<a name="uninstall_docker"></a>

# 二 卸载docker
```shell
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine

rm -rf /etc/systemd/system/docker.service.d

rm -rf /var/lib/docker

rm -rf /var/run/docker
```

# 三 docker启动、重启、关闭命令

| 作用          | 命令       |
| -------------- | ---------------------------- |
| 启动           | systemctl start docker       |
| 守护进程重启   | sudo systemctl daemon-reload |
| 重启docker服务 | systemctl restart  docker    |
| 重启docker服务 | sudo service docker restart  |
| 关闭docker     | service docker stop          |
| 关闭docker     | systemctl stop docker        |
