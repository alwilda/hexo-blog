---
title: SSM整合里的一些配置
author: kinglyq
tags:
- Spring
categories: []
date: 2019-7-13 10:41:20
---
> 注意 是SPRING MYBATIS SPRINGMVC
<!--more-->
# 一 pom.xml和web.xml

## (一) pom.xml

- 记录一下这个神秘代码，否则用的时候到处找还找不到
```xml
<!-- pom.xml -->
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <!-- 文件拷贝时的编码 -->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <!-- 编译时的编码 -->
    <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
</properties>
```

## (二) web.xml

- 这个web.xml使用4.0的，eclipse和idea生成maven项目web.xml都是2.x的版本，不好，不好。
```xml
  <!-- web.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         id="WebApp_ID" version="4.0">

  <display-name>springjson</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.jsp</welcome-file>
  </welcome-file-list>

  <!-- dispatcherServlet -->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:spring/spring-*.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

  <!-- 编码格式UTF-8 -->
  <filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
      <param-name>forceResponseEncoding</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
</web-app>
```
# 二 spring篇

## (一) 将controller层加入component-scan的黑名单

- controller层扫描xxx.xxx.controller,其他包来个 xxx.xxx.*，这样就有点重复，所以在通配那里将controller层加入黑名单
```xml
<context:component-scan base-package="xxx.xxx.*" use-default-filters="false">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```
#  三 mybatis篇

## (一) spring管理mybatis

### 1. spring xml的配置
```xml
<!-- 数据库连接 -->
<!-- <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource"> -->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">	
	<property name="driverClassName" value="${driver}"></property>
	<property name="url" value="${url}"></property>
	<property name="username" value="${username}"></property>
	<property name="password" value="${password}"></property>
</bean>

<!-- 管理MyBatis -->
<bean class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="configLocation"	value="classpath:mybatis-config.xml"></property>
	<property name="dataSource" ref="dataSource"></property>
	<property name="mapperLocations">
		<array>
			<value>classpath:com/xxx/mapper/*.xml</value>
		</array>
	</property>
	<property name="typeAliasesPackage" value="com.xxx.entity"></property>
</bean>

<!-- 管理mapper层接口 -->
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<property name="basePackage" value="com.xxx.mapper"></property>
</bean>
```
### 2. 本身的mybatis-config.xml就配置一下log4j 
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>

	<settings>
		<setting name="logImpl" value="LOG4j" />
	</settings>

	<!-- <plugins>
		<plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
	</plugins> -->

</configuration>
```
### 3. log4j
```yaml
log4j.rootLogger=error, Console  
log4j.logger.com.xxx.mapper=debug  
#Console
log4j.appender.Console=org.apache.log4j.ConsoleAppender  
log4j.appender.Console.layout=org.apache.log4j.PatternLayout  
log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n 
```