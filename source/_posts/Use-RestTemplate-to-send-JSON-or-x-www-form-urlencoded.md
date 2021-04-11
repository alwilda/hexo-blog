---
title: 使用 RestTemplate 发送 JSON 或者 x-www-form-urlencoded
date: 2021-04-11 15:35:25
tags:
categories:
---

二者的区别：

1.  [JSON](https://baike.baidu.com/item/JSON)

    `Content-Type` 被设置为 `application/json`，数据以 `JSON` 格式放在**请求体**中。

<!--more-->

2.  application/x-www-form-urlencoded

    浏览器原生表单默认的编码方式，数据被编码成以 `&` 分隔的键-值对, 同时以 `=` 分隔键和值。 非字母或数字的字符会被 [percent-encoding](https://developer.mozilla.org/zh-CN/docs/Glossary/percent-encoding)：这也就是为什么这种类型不支持二进制数据（应使用 `multipart/form-data` 代替）。

因为数据位置不同，所以后台获取的方式也不同。

---

首先构造一个 `RestTemplate` 实例：

```java
private final RestTemplate restTemplate = new RestTemplate();
```

# JSON

```java
String url = "xxx";

HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.APPLICATION_JSON);

Map<String, Object> params = new HashMap<>(16);
params.put("xxx", "xxx");
params.put...

HttpEntity<Map<String, Object>> request = new HttpEntity<>(params, headers);

// 泛型为接口返回数据的类型
ResponseEntity<Object> response = restTemplate.postForEntity(url, request, Object.class);

// 获取响应主体
response.getBody()；
```

# x-www-form-urlencoded

使用 [`LinkedMultiValueMap`](https://www.javadoc.io/doc/org.springframework/spring-core/latest/org/springframework/util/LinkedMultiValueMap.html) 构造数据。

```java
String url = "http://localhost:6501/api/v1/req-form-urlencoded";

HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.APPLICATION_FORM_URLENCODED);

LinkedMultiValueMap<String, Object> params = new LinkedMultiValueMap<>();
params.add("name", "Martin");
params.add("age", 22);
params.add("gender", true);
params.add...

HttpEntity<LinkedMultiValueMap<String, Object>> request = new HttpEntity<>(params,
        headers);

// 泛型为接口返回数据的类型
ResponseEntity<Object> response = restTemplate.postForEntity(url, request, Object.class);

// 获取响应主体
response.getBody()；
```
