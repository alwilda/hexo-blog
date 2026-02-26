---
title: JavaFX Runtime images (Java 11+)
date: 2021-03-09 16:23:25
tags: JavaFX
categories:
---

JavaFX 项目的 `Runtime images` 是一个自定义 JRE，它仅包含应用程序所需的平台模块。

本文仅针对通过 `Maven` 构建的项目.

<!--more-->

# 起步

构建的成功与否几乎都取决于 `pom.xml` 中关于插件的配置，下面会针对这部分进行阐述。

`javafx-maven-plugin`有两个主要的命令 —— `javafx:run` 和 `javafx:jlink`

- `javafx:run` 进行编译和运行
- `javafx:jlink` 创建自定义运行时

# javafx:run options

可能是原始的情况：

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.8.0</version>
      <configuration>
        <release>11 or 12 13 14 15 ......</release>
      </configuration>
    </plugin>
    <plugin>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-maven-plugin</artifactId>
      <version>0.0.3</version>
      <configuration>
        <mainClass>xxx.xxx.App</mainClass>
      </configuration>
    </plugin>
  </plugins>
</build>
```

参考 [GitHub - openjfx/javafx-maven-plugin: Maven plugin to run JavaFX 11+ applications](https://github.com/openjfx/javafx-maven-plugin#javafxjlink-options) 来进行配置

例如：

```xml
<configuration>
    <stripDebug>true</stripDebug>
    <compress>2</compress>
    <noHeaderFiles>true</noHeaderFiles>
    <noManPages>true</noManPages>
    <launcher>launcher</launcher>
    <jlinkImageName>app</jlinkImageName>
    <jlinkZipName>app</jlinkZipName>
    <mainClass>xxx.xxx.App</mainClass>
</configuration>
```

# 运行 `javafx:run` 的失败情况和解决办法

- `Failed to execute goal org.openjfx:javafx-maven-plugin:0.0.3:run (default-cli) on project hellofx: Error`

  `JAVA_HOME` 与项目需要的版本不一致，为了避免这种情况，可以将正确的版本添加到 `javafx-maven-plugin`:

  ```xml
  <plugin>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-maven-plugin</artifactId>
    <version>0.0.3</version>
    <configuration>
        <executable>xxx\jdk-xxx\bin\java</executable>
    </configuration>
  </plugin>
  ```
