---
title: maven settings.xml
author: kinglyq
tags:
categories: []
date: 2019-8-2 09:13:31
---

仅以此文来保存我的配置

# 一 位置
```xml
<localRepository>E:/MavenStore</localRepository>
```

<!--more-->

# 二 镜像
```xml
<!-- 阿里云镜像 -->
<mirror> 
    <id>alimaven</id> 
    <name>aliyun maven</name> 
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url> 
    <mirrorOf>central</mirrorOf> 
</mirror> 
```

# 三 编码格式与jdk版本
```xml
<!-- 接上面的<profiles>标签 -->

    <profile>    
        <id>jdk-1.8</id>    
        <activation>    
            <activeByDefault>true</activeByDefault>    
            <jdk>1.8</jdk>    
        </activation>    
        <properties>    
            <maven.compiler.source>1.8</maven.compiler.source>    
            <maven.compiler.target>1.8</maven.compiler.target>    
            <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>    
        </properties>    
    </profile>
	
    <!-- 下载源码包 -->
    <profile>
        <id>downloadSources</id>
        <properties>
            <downloadSources>true</downloadSources>
            <downloadJavadocs>true</downloadJavadocs>           
        </properties>
    </profile>

</profiles> <!-- !!! -->
  
<activeProfiles>
    <activeProfile>downloadSources</activeProfile>
</activeProfiles>
```