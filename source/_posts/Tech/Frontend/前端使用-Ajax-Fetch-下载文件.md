---
title: 前端使用 Ajax/Fetch 下载文件
tags: JavaScript
abbrlink: cfde7e65
date: 2021-11-12 10:31:47
categories:
---

有时需要发送大量参数或其它需要而必须用到 POST 请求时

<!--more-->

# 原生 [XMLHttpRequest](https://xhr.spec.whatwg.org/)

```javascript
const xhr = new XMLHttpRequest();
xhr.onload = function (e) {
    const blob = new Blob([xhr.response], { type: "application/octet-stream" }); 
    
    // 可以从 Content-Disposition 中获取文件名
    // const contentDisposition = xhr.getResponseHeader("Content-Disposition");

    let link = document.createElement("a");
    let fileName = "xxx.xxx";    
    link.href = window.URL.createObjectURL(blob);
    link.download = fileName;
    link.click();
    link.remove();
    window.URL.revokeObjectURL(link.href);
}
// GET | POST |...
xhr.open(method, url);
// no param | FormData | json string | ...
xhr.send(params);
```

# 使用 [Fetch](https://attacomsian.com/blog/javascript-fetch-api)

```javascript
fetch(url, {
  method: "POST",
})
.then(resp => resp.blob())
.then(blob => {
  let link = document.createElement("a");
  link.href = window.URL.createObjectURL(blob);
  link.download = "xxx.xxx";
  link.click();
  link.remove();
  window.URL.revokeObjectURL(link.href);
})
```

# 使用 [Axios](https://axios-http.com/zh/)

{% blockquote @Axios https://axios-http.com/zh/docs/intro %}
Axios 是一个基于 promise 网络请求库，在客户端 (浏览端) 中使用 XMLHttpRequests
{% endblockquote %}

```javascript
request({
  url: "",
  method: 'post',
  // 重点
  responseType: 'blob'
}).then((data) => {
  const blob = new Blob([data], { type: 'application/octet-stream' });
  let link = document.createElement('a');
  let fileName = 'xxx.xxx';
  link.href = window.URL.createObjectURL(blob);
  link.download = fileName;
  link.click();
  link.remove();
  window.URL.revokeObjectURL(link.href);
})
```