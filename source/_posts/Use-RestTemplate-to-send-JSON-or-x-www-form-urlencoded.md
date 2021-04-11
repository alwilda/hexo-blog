---
title: 使用 RestTemplate 发送 JSON 或者 x-www-form-urlencoded
date: 2021-04-11 15:35:25
tags:
categories:
---

无论如何先构造一个 `RestTemplate` 实例：

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
