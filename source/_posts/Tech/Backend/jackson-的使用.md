---
title: Java JSON library - Jackson 的使用
tags:
  - Java
  - Jackson
abbrlink: 88ab963a
date: 2021-03-16 10:54:51
---

从实际使用的角度列出对 `Jackson` 的一些操作。

<!--more-->

What is Jackson?

{% blockquote @FasterXML https://github.com/FasterXML/jackson#what-is-jackson GitHub - FasterXML/jackson %}
Jackson has been known as "the Java JSON library" or "the best JSON parser for Java". Or simply as "JSON for Java".
{% endblockquote %}

# 只在序列化或反序列化时忽略

使用注解 `@JsonProperty` 的 `access` 属性。

# 定义反序列化时的别名

使用注解 `@JsonAlias`。

注：可定义属性的一个或**多个**替代名称，在反序列化期间可以接受为**正式名称的替代**。 别名信息在 `POJO` 内省期间也会公开，但在始终使用主名的序列化过程中无效。

代码示例：

```java
public class Info {
    @JsonAlias({ "n", "Name" })
    public String name;
}
```
