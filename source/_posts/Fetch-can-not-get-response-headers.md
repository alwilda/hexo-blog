---
title: Fetch 无法获取响应头
date: 2021-09-23 16:36:04
tags:
categories:
---

请求响应后，打印 [`Response.headers`](https://developer.mozilla.org/zh-CN/docs/Web/API/Response/headers) 却输出了空对象。

<!--more-->

经过笔者数分钟的探索，发现产生这种情况，应该是请求处于**跨域**之中，于此则要在 `fetch()` 中配置 `mode` 属性：

mode: 请求的模式，如 cors、 no-cors 或者 same-origin。

```js
fetch(url,{
    mode: 'cors',
    ...
})
```

至于 `Response.headers` 中的请求头信息不全，则要在服务端配置 `Access-Control-Expose-Headers`。

{% blockquote @MDN https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Expose-Headers Access-Control-Expose-Headers - HTTP | MDN %}
响应首部 `Access-Control-Expose-Headers` 列出了哪些首部可以作为响应的一部分暴露给外部。

默认情况下，只有七种 simple response headers （简单响应首部）可以暴露给外部：

- Cache-Control
- Content-Language
- Content-Length
- Content-Type
- Expires
- Last-Modified
- Pragma

如果想要让客户端可以访问到其他的首部信息，可以将它们在 `Access-Control-Expose-Headers` 里面列出来。
{% endblockquote %}

