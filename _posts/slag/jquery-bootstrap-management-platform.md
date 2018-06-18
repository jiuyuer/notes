---
title: Jquery+Bootstrap构建传统后台管理系统
tags:
  - JavaScript
  - 前端开发
categories:
  - 技术渣
date: 2017-09-10 16:43:34
---

现在流行的是前后端分离，MV\*模式，我作为一个相对传统行业的老菜鸟来说说最近手上的一个后台管理系统项目的前端工作，欢迎提各种意见。

### 项目背景

- 传统后台管理系统，面向的是企业级客户，兼容 IE8+等主流浏览器，所以对界面友好程度相对来说并不是太大，你懂得

### 前端框架(类库)

- Jquery+Bootstrap+Layer+zTree+Validform

谈框架这种高大上的东西，我更想用类库来表达(恩，因为我觉得自己对框架这个概念的认识还很浅)，没错正如标题所言，由 jq+bootstrap 构建，再新增一个皮肤包，根据 UI 出的视觉稿进行编码，就将其称为个性化，换肤功能吧。

### 公共 CSS

在 css 公共调用上，我又添加了一些简单字体大小，间距等等

#### 定位

```css
.pos-r {
  position: relative;
}
.pos-a {
  position: absolute;
}
.pos-f {
  position: fixed;
}
```

#### 文字溢出省略号

```css
.single-overflow {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.text-overflow {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  padding: 0 2px;
}
```

<!-- more -->

#### 文字尺寸

```css
.f-12 {
  font-size: 12px;
}
.f-14 {
  font-size: 14px;
}
.f-16 {
  font-size: 16px;
}
.f-18 {
  font-size: 18px;
}
.f-20 {
  font-size: 20px;
}
.f-25 {
  font-size: 25px;
}
.f-30 {
  font-size: 30px;
}
.f-40 {
  font-size: 40px;
}
.f-50 {
  font-size: 50px;
}
```

#### 文字颜色

```css
.c-red,
.c-red a,
a.c-red {
  color: #f00;
}
.c-green,
.c-green a,
a.c-green {
  color: #008000;
}
.c-blue,
.c-blue a,
a.c-blue {
  color: #00f;
}
.c-white,
.c-white a,
a.c-white {
  color: #fff;
}
.c-black,
.c-black a {
  color: #333;
}
.c-black a:hover {
  color: #f60;
}
.c-gray,
.c-gray a,
a.c-gray {
  color: #808080;
}
.c-666,
.c-666 a,
a.c-666 {
  color: #666;
}
.c-999,
.c-999 a,
a.c-999 {
  color: #999;
}
.c-orange,
.c-orange a,
a.c-orange {
  color: #ffa500;
}
```

#### 间距 padding/margin

```css
.ml-5 {
  margin-left: 5px !important;
}
.mr-5 {
  margin-right: 5px !important;
}
.mt-5 {
  margin-top: 5px !important;
}
.mb-5 {
  margin-bottom: 5px !important;
}

/*.pl-5，.pt-5，pb-5，pr-5 等等以此类推*/
```

---

### 类库说明

#### Bootstrap

- Modal，主要用来做异步请求时的表单操作，像增，改。
- bootstrapTable，个人认为是整个系统的主体，后台系统大多数据展示是以表格形式来视图化，然后这个接口已然够用。有些个性化的东西，在此基础上再进行开发，也就方便，比如，列表表单的显示个性化，可以通过 h5 的 localstorage 进行本地存储，这里在开发过程中碰到一个小坑，在 IE 下面好像没法直接将原来存储的数据清除，只能使用 localstorage.clear()方法？chremo 下面可以在开发工具下直接删除
- 然后就是 bootstrap 上应用到的个个小组件啦，自行去官网看 api 吧

#### Layer

- 作为提示控件来使用，关于 api 啥的也自行前往官网查看

#### zTree

- 系统中涉及到的树形结构就用 zTree，调用时使用列表形式的 json 数据格式进行交互，最好使用异步的展示形式，不然大数据时会影响性能

#### Validform

- Validform 用来表单的校验，一般都是通过 ajax 来进行表单提交，所以我把 ajax 都封装在了 beforeSubmit 这个接口中，还有一个要说明一下，因为错误提示可能需要自定义，可在 tiptype 中进行修改，还有一个就是考虑表单防重复提交

#### 公共的 js 类库

我目前是通过单体模式进行封装的

```javascript
var Project = {
  //公共模块
  Util: {
    util_method1: function() {
      console.log('util_method1');
    },
    util_method2: function() {
      console.log('util_method2');
    }
  },
  //工具模块
  Tool: {
    tool_method1: function() {
      console.log('tool_method1');
    },
    tool_method2: function() {
      console.log('tool_method2');
    }
  },
  //其他模块，ajax等
  Others: {}
};
```

### 综上所述

那么我觉得一个传统的后台系统开发基本够用了，最后可能需要处理一下前端上的性能，比如，将静态资源打包压缩成一个文件，这里其实还有一个小坑，就是在 IE9 以下的低版本，如果你打包出来的一个 css 文件过大（内容过多），那么 IE9 及以下版本的部分 css 样式就不会生效啦，这时就需要做 hack 处理。

### 题外话

作为前端来说，我感觉上述这种系统做多了，会麻木，失去新鲜感。我还是更喜欢互联网模式的开发节奏，用市面上一些比较流行的框架，像 vue,react 等，前后端分离，各种打包工具(gulp，webpack)，模块化及组件化开发。像我上述这种开发模式，就自己所学的新东西并不能真正意义上用到目前的项目中，只能自己写些 demo，作为约束能力薄落的我来说，进步并不太明显，所以，最近也在考虑寻找新东家，希望能去互联网行业，对技术要求更高的公司继续自己的职业，提升自己的技术水平。求推荐啊！

<br>
<br>
