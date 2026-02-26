---
title: 使用 MyBatis-Plus 更新字段为 null 值时报错
tags:
  - MyBatis
  - MyBatis-Plus
abbrlink: b3ab85e5
date: 2023-11-18 10:57:52
categories:
---

事情发生在使用 **Oracle 数据库** 时，通过 `UpdateWrapper` 更新一个字段为 null 时报了如下错误：

```
org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.type.TypeException: Could not set parameters for mapping: ParameterMapping{property='ew.paramNameValuePairs.MPGENVAL1', mode=IN, javaType=class java.lang.Object, jdbcType=null, numericScale=null, resultMapId='null', jdbcTypeName='null', expression='null'}. Cause: org.apache.ibatis.type.TypeException: Error setting null for parameter #1 with JdbcType OTHER . Try setting a different JdbcType for this parameter or a different jdbcTypeForNull configuration property. Cause: java.sql.SQLException: 无效的列类型: 1111
```

<!--more-->

解决方法就是设置正确的 `jdbcTypeForNull` 值。

```yml
mybatis-plus:
    # 必须使用引号包裹，不然就是 set(null) 而不是 set('NULL')
    jdbc-type-for-null: 'null' 
```

关于 `jdbcTypeForNull` 的官方描述：

{% blockquote @MyBatis https://mybatis.org/mybatis-3/zh/configuration.html#设置（settings） %}
| 设置名 | 描述 | 有效值 | 默认值 |
|  ----  | ----  | ---- | ---- |
| jdbcTypeForNull | 当没有为参数指定特定的 JDBC 类型时，空值的默认 JDBC 类型。 某些数据库驱动需要指定列的 JDBC 类型，多数情况直接用一般类型即可，比如 NULL、VARCHAR 或 OTHER。 | JdbcType 常量，常用值：NULL、VARCHAR 或 OTHER。 | OTHER |
{% endblockquote %}

<br />

这样便可以使用 `Wrapper` 去更新字段为 null 值。

```java
Wrapper<StudentEntity> updateWrapper = Wrappers.lambdaUpdate(Student.class)
                .set(StudentEntity::getName, null)
                .eq(StudentEntity::getId, 1);
```

如果想通过实体类去更新呢？
则可以通过配置 updateStrategy 为 `ALWAYS` 实现。

```java
@TableField(updateStrategy = FieldStrategy.ALWAYS)
private String name;
```

```java
Student student = new Student();
student.setId(1L);
student.setName(null);
studentService.updateById(student);
```

在 **MySQL** 上测试，发现无需额外设置 `jdbcTypeForNull` 也可更新字段为 `null`。