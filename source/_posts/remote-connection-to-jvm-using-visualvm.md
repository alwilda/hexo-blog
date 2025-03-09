---
title: 使用 VisualVM 远程连接 JVM
date: 2022-12-06 15:35:26
tags: Java
categories:
---

# 修改 Java 配置

<!--more-->

1. 首先进入 `${JAVA_HOME}/jre/lib/management/` (Java8 之后在 `/conf/management`) 目录。

2. 重命名 *jmxremote.password.template*。

```shell
cp jmxremote.password.template jmxremote.password
```

3. 修改该文件，去掉如下内容的注释。

```shell
monitorRole  QED
controlRole  R&D
```

# 添加运行参数

如果使用 tomcat 就修改 bin/catalina.sh (.bat) 文件添加参数。

``` shell
# 在 tomcat的 bin 目录下，修改 catalina.sh，添加如下参数
JAVA_OPTS="
-Dcom.sun.management.jmxremote 
-Dcom.sun.management.jmxremote.port=9999
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false"
```

使用 jar 包启动就在启动时添加参数：

启动参数示例：

```shell
java 
-Dcom.sun.management.jmxremote 
-Dcom.sun.management.jmxremote.port=9999 
-Dcom.sun.management.jmxremote.local.only=false 
-Dcom.sun.management.jmxremote.authenticate=false  
-Dcom.sun.management.jmxremote.ssl=false 
-Djava.rmi.server.hostname= your server host 
-jar xxx.jar
```

 JMX Server 还会随机额外的去监听两个端口，所以在远程连接时我们本地的JMX在连接时也会尝试去连接监听端口。

 ```shell
 jps -l

 lsof -i|grep xxx
 ```

|                     参数                     |                                 说明                                  |
| -------------------------------------------- | --------------------------------------------------------------------- |
| -Dcom.sun.management.jmxremote               | 允许使用 JMX 远程连接                                                  |
| -Dcom.sun.management.jmxremote.port          | 指定 JMX 启动的代理端口，即 visualvm 要连接的端口                        |
| -Dcom.sun.management.jmxremote.local.only    | 只允许本地连接                                                         |
| -Dcom.sun.management.jmxremote.authenticate  | 指定了JMX是否启用鉴权（需要用户名，密码鉴权）                            |
| -Dcom.sun.management.jmxremote.ssl           | 指定 JMX 是否启用 ssl                                                  |
| -Djava.rmi.server.hostname                   | 指定服务器主机名                                                       |
| -Dcom.sun.management.jmxremote.rmi.port      | 将这个端口和 jmx.port 的端口设置成一个端口，这样防火墙就只需要放行一个端口 |
| -Dcom.sun.management.jmxremote.access.file   | 用户权限文件路径                                                       |
| -Dcom.sun.management.jmxremote.password.file | 密码文件路径                                                           |

通过以上配置便可以在 VisualVM 中使用 JMX 连接。

