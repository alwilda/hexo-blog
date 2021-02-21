---
title: 普通Java项目读取properties文件
author: kinglyq
date: 2019-05-25 11:53:48
tags: []
categories: []
---
> 后缀properties是一种属性文件。
这种文件以key=value格式存储内容。
Java中可以使用Properties类来读取这个文件。
String value=p.getProperty(key);就能得到对应的数据。
一般这个文件作为一些参数的存储，代码就可以灵活一点。

<!--more-->

```java
package priv.lyq.test;

import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

import javax.xml.transform.Source;

import org.junit.jupiter.api.Test;

import com.sun.org.apache.xalan.internal.xsltc.compiler.SourceLoader;

public class ReadProperties {

	@Test
	public void test1() {
		Properties pop = new Properties();
		
		/* InputStream input=new FileInputStream(new File(pathfileName));*/ // 绝对路径

		InputStream input = Thread.currentThread().getContextClassLoader().getResourceAsStream("db.properties");
		try {
			pop.load(input);
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			System.out.println(pop.get("driver"));
			System.out.println(pop.get("url"));
			System.out.println(pop.get("username"));
			System.out.println(pop.get("password"));
		}

	}

	@Test
	public void test2() {
		Properties pop = new Properties();
		// InputStream input = SourceLoader.class.getResourceAsStream("db.properties");
		InputStream input = ClassLoader.getSystemResourceAsStream("db.properties");
		try {
			pop.load(input);
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			System.out.println(pop.get("driver"));
			System.out.println(pop.get("url"));
			System.out.println(pop.get("username"));
			System.out.println(pop.get("password"));
		}
	}

	/*end*/
}
```