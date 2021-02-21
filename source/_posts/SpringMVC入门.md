---
title: SpringMVC入门
author: kinglyq
tags:
- Spring
- Spring MVC
categories: []
date: 2019-06-30 23:57:52
---

# 一 SpringMVC流程

## (一) 什么是MVC模式

+ MVC是一种设计模式

    - M-Model 模型（完成业务逻辑：有javaBean构成，service+dao+entity）

    - V-View 视图（做界面的展示  jsp，html……）

    - C-Controller 控制器（接收请求—>调用模型—>根据结果派发页面）
	

<!--more-->

![](MVC过程.png)
　
## (二) 流程叙述

1. 用户发送请求至前端控制器DispatcherServlet。

2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。

3.  处理器映射器找到具体的处理器(可以根据xml配置、注解进行查找)，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。

4. DispatcherServlet调用HandlerAdapter处理器适配器。

5. HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。

6. Controller执行完成返回ModelAndView。

7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet。

8.  DispatcherServlet将ModelAndView传给ViewReslover视图解析器。

9. ViewReslover解析后返回具体View。

10. DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。

11.  DispatcherServlet响应用户。

![](SpringMVC流程.png)

# 二 Web项目启动加载配置文件

## (一) xml配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         id="WebApp_ID" version="4.0">

    <display-name>xxx</display-name>

    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!--
        &lt;!&ndash; 非SpringMVC项目加载配置文件 &ndash;&gt;
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>
                classpath:applicationContext.xml
            </param-value>
        </context-param>
    
        <listener>
            &lt;!&ndash; 此监听器在服务器启动丝毫初始化IOC容器 &ndash;&gt;
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
    -->

    <servlet>
        <!--
            如果没有写加载xml的初始化参数的话
            这个servlet-name叫springmvc，则SpringMVC会自动加载WEB-INF下springmvc-servlet.xml,
            如果换作其他名字比如叫dispatcherServlet,则会加载dispatcherServlet-servlet.xml
        -->
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
         <init-param>
             <param-name>contextConfigLocation</param-name>
             <param-value>classpath:spring-*.xml</param-value>
         </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

## (二) classpath 和 classpath* 的区别

> 一般classpath指向的是classes，也就是编译路径的根路径，而一般classes中放着这些文件:
> 1.java文件编译好的class文件。
> 2.properties配置文件。
> 3.xml配置文件。
> 4.一些模版文件，如*.ftl。
> 5.其他需要用classpath获取到的文件。

1. classpath：只会到你指定的class路径中查找文件;

2. classpath*：不仅包含class路径，还包括jar文件中(class路径)进行查找。


# 三 配置视图解析器
```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
```


# 四 @RequestMapping注解

## (一) 属性解释

> @RequestMapping('xxx') 默认不加任何属性,为请求的路径，可以加到类上。

### 1. method 设置请求的方式
```
method = {RequestMethod.GET,RequestMethod.POST}
```

### 2. params 请求的参数的设置
```
params = {"name"} // 请求参数必须包含 name
params = {"name=abc"} // 请求参数name必须等于abc
params = {"age!=18"} // 请求参数age的值不能是18
params = {"!gender"} // 请求参数不能有 gender
```

### 3. headers 请求头信息的设置
```
headers = {}
```

## (二) Ant风格的请求路径

### 1. 什么是Ant风格

通配符 | 说明
:-:|-
? | 匹配任何单字符
\* | 匹配0或者任意数量的字符
** | 匹配0或者更多的目录

### 2. 通配符*

任意字符
```html
 @RequestMapping(value = "s1/*/get1")

 <a href="${pageContext.request.contextPath}/s1/abcdefg/get1?msg=common">*通配符</a>
```

### 3. 通配符**

任意目录
```html
 @RequestMapping(value = "s2/**/get2")

 <a href="${pageContext.request.contextPath}/s2/a/b/c/get2?msg=common">**通配符</a>
```

<a name='PathVariable'></a>

## (三) @PathVariable接受动态参数
```java
 @RequestMapping(value = "s3/*/get3/{name}", method = {RequestMethod.GET})
    public String get2(@PathVariable("name") String name) {
        System.out.println(name);
        return "success.jsp";
    } 
    // name = "antStyle"
```

```html
<a href="${pageContext.request.contextPath}/s3/abc/get3/antStyle">ant传</a>
```

# 五 Result风格

## (一) 过滤的条件

1. ``<input type="hidden" name="_method" value="delete/put" />``

2. 请求方式是POST

## (二) web.xml的配置
```xml
<!-- Result风格 过滤器配置 -->
<filter>
    <filter-name>hiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>hiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

## (三) 实例
1. input标签value值必须是大写

```java
@RequestMapping(value = "test/{id}", method = {RequestMethod.DELETE})
public String delete(@PathVariable("id") String id) {
    System.out.println(id);
    return "success.jsp";
}
```

```html
<form action="" method="post">
    <input type="hidden" name="_method" value="DELETE" />
    <input type="submit" value="删除" />
</form>
```
PUT同理

**当映射名称都相同时，可以通过不同的Method指定不同的请求**

# 六 数据接收的几种方式

## (一) 表单数据与后台方法形参对应

1. 适用于get方式提交，不适用于post方式提交。
2. 参数name值名最好和后台形参名保持一致。

```java
@RequestMapping("/addUser1")
public String addUser1(String username,String password) {
    System.out.println("username is:"+username);
    System.out.println("password is:"+password);
    return "xxx";
}
```

```html
<form method="GET" action="addUser1">
    用户名：<input type="text" name="username" />
    密码：<input type="password" name="password" />
    <input type="submit " value="提交" />
</form>
```

### 1. @RequestParam注解

这个也可算是一种新的接收方式
1. 可以对传入参数指定参数名。
2. 可以通过required=false或者true来要求@RequestParam配置的前端参数是否一定要传。 
3. 如果@requestParam注解的参数是int类型，并且required=false，此时如果不传参数的话，会报错。原因是，required=false时，不传参数的话，会给参数赋值null，这样就会把null赋值给了int，因此会报错。
4. defaultValue="" 设置默认值。

## (二) 通过HttpServletRequest接收

不再赘述

## (三) 通过JavaBean(实体类)接收

1. 支持级联。比如：

```java
public class User {
    private String username;
    private String password;
    private Address address;
}
public class Address {
    private Integer addressId;
    private Integer userId;
    private String username;
    private String province;
    private String city;
    private String county;
    private String address;
    private String tel;
}
```

```html
<input type="text" name="address.province" />
```

## (四) @PathVariable接受动态参数

<a href="#PathVariable">上面已经解释，点击查看</a>

## (五) 使用@ModelAttribute注解获取POST请求的FORM表单数据

```java
 @ModelAttribute
public void getAccount(Map<String, Account> map) {
    Account account = new Account(1, "jack", 25.0);
    map.put("account", account); // map的key就是方法参数类型的首字母小写
    System.out.println("getAccount" + account);
}

@RequestMapping(value = "updateAccount", method = RequestMethod.POST)
public ModelAndView updateAccount(@ModelAttribute("acc") Account account) {
    ModelAndView mv = new ModelAndView("");
    return null;
}
```

1.  如果map的key和方法参数类型的首字母小写不一致，则用@ModelAttribute("acc")注解保持一致

```html
<form action="${pageContext.request.contextPath}/model/updateAccount" method="post">
    <input type="hidden" name="id" value="1"/>
    name:<input type="text" name="name"/><br><br>
    money:<input type="text" name="money"/><br><br>
    <input type="submit" value="提交"/>
</form>
```
**注意**
1. 被@ModelAttribute注释的方法会在此controller每个方法执行前被执行，因此对于一个controller映射多个URL的用法来说，要谨慎使用。

# 七 处理数据模型

> 与传统的Servlet将数据放到request域通过转发带到jsp无异

## (一) ModelAndView

## (二) ModelMap

## (三) Model

## (四) Map

## (五) 将数据放到session中

> 默认情况下Spring MVC将模型中的数据存储到request域中。当一个请求结束后，数据就失效了。如果要跨页面使用。那么需要使用到session。而@SessionAttributes注解就可以使得模型中的数据存储一份到session域中。

- @SessionAttributes参数
    1. names：这是一个字符串数组。里面应写需要存储到session中数据的名称。

    2. types：根据指定参数的类型，将模型中对应类型的参数存储到session中

    3. value：其实和names是一样的。

例：@SessionAttributes(types = {User.class}) 将所有User类型放到session中

- 　如果想删除session中共享的参数，可以通过SessionStatus.setComplete()，这句只会删除通过@SessionAttribute保存到session中的参数

**【注意】：@SessionAttributes注解只能在类上使用，不能在方法上使用**

# 八 国际化

## (一). 编写properties文件

![](i18n_1.jpg)

![](i18n_2.jpg)

## (二). xml配置

```xml
	<!-- 国际化 -->
	<bean id="messageSource" 			class="org.springframework.context.support.ResourceBundleMessageSource">
		<property name="basename" value="i18n"></property>
		<property name="defaultEncoding" value="UTF-8"></property>
	</bean>
	
	<!-- id不能不写 -->
	<bean id="localeResolver" class="org.springframework.web.servlet.i18n.CookieLocaleResolver"></bean>
	
	 <!-- 该拦截器通过名为”lang”的参数来拦截HTTP请求，使其重新设置页面的区域化信息 -->
	<mvc:interceptors>
		<bean class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor">
			<property name="paramName" value="lang"></property>
		</bean>
	</mvc:interceptors>
```



## (三). controller
```java
@RequestMapping(value = "lang")
public String lang(){
	return "index.jsp";
}
```

