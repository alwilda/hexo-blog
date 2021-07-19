---
title: 让 VS Code 准确识别 maven 项目的 Java 版本
date: 2021-07-18 23:12:18
tags: Visual Studio Code
categories:
---

在 `pom.xml` 中通过 [`maven-compiler-plugin`](http://maven.apache.org/plugins/maven-compiler-plugin/examples/set-compiler-source-and-target.html) 插件来配置 `Java` 版本，这样 VS Code 才能正确识别并使用相应版本的 `JDK`。

<!--more-->

{% codeblock lang:xml pom.xml %}
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-compiler-plugin</artifactId>
	<version>3.8.1</version>
	<configuration>
		<source>11</source>
		<target>11</target>
	</configuration>
</plugin>
{% endcodeblock %}