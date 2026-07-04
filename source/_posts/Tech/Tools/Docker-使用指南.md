---
title: Docker 使用指南
abbrlink: 4fbde0fb
date: 2026-07-02 21:02:38
tags:
categories:
---

# 安装与配置

## Ubuntu

1. 清理旧版本（可选）
   如果系统之前安装过旧版本的 Docker（如 docker、docker-engine 或 docker.io），建议先卸载干净：

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

<!--more-->

2. 安装前置基础软件
   更新 apt 包索引并安装一些允许 apt 通过 HTTPS 使用仓库的必要工具：

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
```

3. 添加 Docker 官方 GPG 密钥
   为了确保下载的软件安全正宗，需要添加 Docker 的官方密钥：

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

4. 设置 Docker 稳定版仓库
   将 Docker 仓库添加到你的系统软件源列表中：

{% tabs First unique name %}
<!-- tab 清华源 -->

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list >/dev/null
```

<!-- endtab -->

<!-- tab 官方源 -->

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list >/dev/null
```

<!-- endtab -->
{% endtabs %}

5. 安装 Docker Engine
   更新 apt 源索引，并安装最新版的 Docker Engine、命令行和 Containerd：

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

6. 验证安装是否成功
   运行一个经典的 hello-world 镜像来测试 Docker 是否正常工作：

```bash
sudo docker run hello-world
```

如果看到 `Hello from Docker!` 的欢迎提示，说明 Docker 已经成功安装并运行了。

## 进阶配置（推荐）

1. 非 root 用户免 sudo 运行 Docker
   默认情况下，运行 docker 命令必须加上 sudo。如果你不想每次都输 sudo，可以把当前用户加入 docker 用户组：

```bash
sudo usermod -aG docker $USER
```

注意：激活该配置需要注销并重新登录系统，或者运行 `newgrp docker` 来立即生效。

2. 设置开机自启
   让 Docker 随系统启动而自动运行：

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

## 配置 Registry Mirror

编辑 Docker 的配置文件（如果文件不存在会自动创建）：

```bash
sudo mkdir -p /etc/docker
sudo nano /etc/docker/daemon.json
```

在文件中粘贴以下内容（这里包含了目前国内一些主流、仍在维护的镜像源）：

```json
{
  "registry-mirrors": [
    "https://2a6bf1988cb6428c877f723ec7530dbc.mirror.swr.myhuaweicloud.com",
    "https://docker.1panel.live",
    "https://hub.rat.dev",
    "https://docker.m.daocloud.io",
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com",
    "https://your_preferred_mirror",
    "https://dockerhub.icu",
    "https://docker.registry.cyou",
    "https://docker-cf.registry.cyou",
    "https://dockercf.jsdelivr.fyi",
    "https://docker.jsdelivr.fyi",
    "https://dockertest.jsdelivr.fyi",
    "https://mirror.aliyuncs.com",
    "https://dockerproxy.com",
    "https://mirror.baidubce.com",
    "https://docker.m.daocloud.io",
    "https://docker.nju.edu.cn",
    "https://docker.mirrors.sjtug.sjtu.edu.cn",
    "https://docker.mirrors.ustc.edu.cn",
    "https://mirror.iscas.ac.cn",
    "https://docker.rainbond.cc"
  ]
}
```

配置好 daemon.json 后，必须重启 Docker 服务才能生效：

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

检查是否配置成功：

```bash
docker info | grep -A 4 "Registry Mirrors"
```

如果输出中看到了刚刚配置的网址，就说明以后 docker pull 就会通过这些加速通道下载了！

# 常用命令

## 镜像管理命令

| 命令              | 作用                    | 示例                            |
|-----------------|-----------------------|-------------------------------|
| `docker pull`   | 从仓库下载镜像到本地            | `docker pull nginx:latest`    |
| `docker images` | 查看本地已下载的所有镜像          | `docker images`               |
| `docker rmi`    | 删除本地镜像 (Remove Image) | `docker rmi nginx`            |
| `docker build`  | 通过 Dockerfile 构建一个新镜像 | `docker build -t myapp:v1 .`  |
| `docker tag`    | 给镜像打标签/重命名            | `docker tag nginx mynginx:v1` |

## 容器生命周期管理

| 命令            | 作用           | 常用参数与示例                                                                                                      |
|---------------|--------------|--------------------------------------------------------------------------------------------------------------|
| `docker run` | 创建并启动一个新容器 | `docker run -d -p 8080:80 --name my-nginx nginx` <br/> -d: 后台运行 <br/> -p: 端口映射 (宿主机:容器) <br/> --name: 自定义容器名 |
| `docker ps`   | 列出正在运行的容器    | `docker ps`（加上 `-a` 可以看到包括已停止的所有容器）                                                                          |
| `docker stop` | 停止一个运行中的容器   | `docker stop my-nginx`                                                                                       |
| `docker start` | 启动一个已经停止的容器  | `docker start my-nginx`                                                                                      |
| `docker restart` | 重启容器         | `docker restart my-nginx`                                                                                    |
| `docker rm`   | 删除一个容器       | `docker rm my-nginx`（正在运行的容器需要加 `-f` 强制删除）                                                                   |

## 容器运维与监控

| 命令              | 作用                   | 常用参数与示例                                   |
|-----------------|----------------------|-------------------------------------------|
| `docker exec` | 进入容器内部执行命令        | `docker exec -it my-nginx /bin/bash`      |
| `docker logs` | 查看容器运行产生的日志          | `docker logs -f --tail 100 my-nginx`      |
| `docker inspect` | 查看容器的详细配置信息 (元数据)    | `docker inspect my-nginx`                 |
| `docker stats`  | 动态查看容器占用 CPU、内存等资源的情况 | `docker stats`                            |
| `docker cp`     | 在宿主机和容器之间复制文件        | `docker cp /path/file.txt my-nginx:/tmp/` |

## 系统清理（释放磁盘空间）

- 查看 Docker 磁盘占用情况：

```bash
docker system df
```

- 一键深度清理（更安全、更干净）
  如果不仅想删除镜像，还想把未使用的容器、网络和挂载卷一起清理掉，可以使用 Docker 自带的系统清理命令：

```bash
docker system prune -a --volumes
```

如果只是想精准打击那些下载不完整、或者被覆盖导致变成 `<none>` 的镜像碎片，可以使用专门的镜像清理命令：

```bash
docker image prune
```

## 导入导出镜像

- 导出命令

```bash
docker save -o [导出的文件名.tar] [镜像名称:版本号]
```

- 导入命令

```bash
sudo docker load -i [导出的文件名.tar]
```