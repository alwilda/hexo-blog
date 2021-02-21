---
title: VMware中Centos7的联网
author: kinglyq
tags:
- Centos7
categories: []
date: 2019-02-09 14:40:00
---
## VMware的设置
1. 首先：打开虚拟机的编辑菜单，选择“虚拟机网络编辑器”，点击更改设置
2. 在虚拟机网络编辑器中选择还原默认设置

<!--more-->

## Linux的设置
在这里需要注意的是必需以**root用户**来登录进行设置
1. 输入 ls /etc/sysconfig/network-scripts，查看该虚拟机的网络信息。
2. 接着在终端输入vi /etc/sysconfig/network-scripts/ifcfg-ensXXXX，此时进入ifcfg-ensXXXX这个网络配置文件的阅读模式。
3. 接着按i键，进入文本插入编辑模式，重点设置BOOTPROTO=dhcp，ONBOOT=yes即可。
4. 修改完之后，先按Esc键，再输入 :wq ，最后按回车键方可退出vim编辑器。

## 开启VMware相关服务
1. 新建一个bat文件，输入：
{% codeblock %}
net start "VMware DHCP Service"
net start "VMware NAT Service"
pause
{% endcodeblock %}
2. 以管理员身份运行。
3. 虚拟机的终端中输入 service network restart，回车确认重启network服务。

*使用 ping 命令或者 ping -c 数字 测试是否能联网*