---
title: Java @SuppressWarnings 注解
tags: Java
abbrlink: b266ff9a
date: 2021-07-17 13:19:41
categories:
---

{% blockquote Java Docs https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html SuppressWarnings (Java Platform SE 8 ) %}
指示应在带注释的元素（以及带注释的元素中包含的所有程序元素）中抑制指定的编译器警告。
{% endblockquote %}

<!--more-->

这个注解是危险的，因为警告是代码中潜在的错误。因此，如果我们收到任何警告，首先应该是解决这些错误。但是如果我们要压制任何警告，我们必须有一些充分的理由，在每次使用时都应该注释上原因。

`@SuppressWarnings` 注解内可用的值如下：

| 值          | 描述                                                    |
| ----------- | ------------------------------------------------------- |
| all         | 抑制所有警告                                            |
| unchecked   | 执行了未检查的类型转换时的警告                          |
| unused      | 未使用的变量                                            |
| deprecation | 使用已弃用的方法或类型                                  |
| divzero     | 除以零警告                                              |
| serial      | 可序列化的类上缺少 serialVersionUID                     |
| fallthrough | 当 Switch 程序块直接通往下一种情况而没有 break 时的警告 |
| cast        | 从泛型类型转换为非限定类型或其他方式时抑制警告          |
| empty       | 忽略带有空函数的语句的警告                              |
| rawtypes    | 没有传递带有泛型的参数                                  |
| try         | 没有 catch 时的警告                                     |
| finally     | 避免与不返回的 finally 块相关警                         |
