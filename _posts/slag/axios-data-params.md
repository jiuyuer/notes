---
title: Axios发送请求时params和data的区别
tags:
  - Javascript
  - ajax
  - axios
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
  url:
    'https://onana.cn/openapi/api?info=20ff1803ff65429b8',
  params: {
    info: '西安天气'
  }
})
```

如果我们将 params 修改为 data，那么是不能请求成功的，因为 get 请求中不存在 data 这个选项。

<br/>