---
title: Axios发送请求时params和data的区别
tags:
  - JavaScript
  - Ajax
  - Axios
categories:
  - 技术渣
date: 2018-06-14 13:44:27
---

在使用 axios 时，注意到配置选项中包含 params 和 data 两者，以为他们是相同的，实则不然。

因为 params 是添加到 url 的请求字符串中的，用于 get 请求。

而 data 是添加到请求体(body)中的， 用于 post 请求。

比如对于下面的 get 请求：

```javascript
axios({
  method: 'get',
  url: 'https://onana.cn/openapi/api?info=20ff1803ff65429b8',
  params: {
    info: '西安天气'
  }
})
```

如果我们将 params 修改为 data，那么是不能请求成功的，因为 get 请求中不存在 data 这个选项。

#### Tip:

> HTTP 请求过程中

- GET 请求：表单参数以 name=value&name1=value1 的形式附到 url 的后面

- POST 请求：表单参数是在请求体中，也是 name=value&name1=value1 的形式在请求体中。

- POST 表单请求提交时，使用的 Content-Type 是 application/x-www-form-urlencoded，而使用原生 AJAX 的 POST 请求如果不指定请求头 RequestHeader，默认使用的 Content-Type 是 text/plain;charset=UTF-8。在 html 中 form 的 Content-type 默认值：Content-type：application/x-www-form-urlencoded。如果使用 ajax 请求，在请求头中出现 request payload 导致参数的方式改变了，那么解决办法就是：

  > headers: {'Content-Type':'application/x-www-form-urlencoded'}

这样，问题就可以解决。

<br/>
