---
title: Vue+Webpack在Template中为Img标签的属性Src赋值问题
tags:
  - JavaScript
  - Vue.js
categories:
  - 技术渣
date: 2018-07-04 00:48:17
---

使用 Vue 的脚手架构建项目过程中，其中一个模板是这样写的：

```html
<template>
  <div>
    <a href="#">
      <img :src="imgSrc">
    </a>
  </div>
</template>
```

大致代码如上所示，其实 imgSrc 是一个变量方式引入的图片地址。

遇到的问题是 imgSrc 中的路径并不会被 webpack 编译，还保持着相对路径的状态，最终产生 404 错误。

那该如何解决？

#### 如果使用的是 img 标签

```javascript
// js 中代码
data () {
    return {
        img: require('path/to/your/source')
    }
}
```

```html
<!-- 然后在template中 -->
<img :src="img" />
```

#### 如果使用的是背景图的方式

```javascript
// js 中代码
data () {
    return {
        img: require('path/to/your/source')
    }
}
```

```html
<!-- html 中代码 -->
<div :style="{backgroundImage:'url(' + img + ')'}"></div>
```

```css
/* 或者直接在css中定义 */
.img {
  background-image: url('path/to/your/source');
}
```

通过 require 的方式去加载，就能让 webpack 编译并在生产版本中正常展示
