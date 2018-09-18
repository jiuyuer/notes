---
title: 移动端fixed的元素抖动问题
tags:
  - HTML5
  - Css/Css3
categories:
  - 技术渣
date: 2018-09-18 21:22:43
---

工作中发现，给一个元素添加 `fixed` 属性，让它固定在窗口某个位置，直接加 `position:fixed` 这个属性就能重现这个效果（BUG）；

在安卓手机上的效果都比较好，但是 ios 系统的个别浏览器兼容性就不好，如 QQ 浏览器、UC 浏览器、360 浏览器（这几个是 ios 最容易出问题的浏览器）；

## 问题重现：

当用户快速滑动页面的到时候，fixed 的元素就会在窗口跳动或者抖动，非常影响用户体验

## 解决方案：

大致思路就是，**将 fixed 的元素与滚动的元素区分开来**，例如：项目中有一个固定在底部的使用了 fixed 的按钮，那么滚动的容器与之成为兄弟元素

```html
<div class="container">
  <!-- 这里是内容区的滚动 -->
  <div class="content">
    <p>...</p>
    <!-- 很长的内容 -->
    <p>...</p>
  </div>
  <!-- 这里是固定底部的按钮或者其他元素 -->
  <div class="fixBox">
    <button>按钮</button>
  </div>
</div>
```

```css
.container {
  width: 100%;
  height: 100%;
  overflow: hidden;
  display: flex;
}
.content {
  flex: 1 1 auto;
  overflow: auto;
  overflow-x: visible;
}
.fixBox {
  position: absolute;
  bottom: 0;
  height: 45px;
  width: 100%;
}
```

> 在 class 为 container 的内容层中滚动，实际上，滚动条在 content 上，与 fixBox 已经无关，所以就不会影响抖动问题

## 额外出现的问题

精确定位到问题所在之后，就开始写 HTML 跟 CSS 了，因为考虑到是在移动端的项目，所以二话不说，直接上了 flex 的布局。

结果，测试人员在测试的过程中发现，**低版本 webview 不支持 css3 flex 布局**，具体请 [点这里](https://caniuse.com/#search=flex).

尴了个尬，此处省略无数个 WTF~!

最后，只能使用最原始的绝对定位来实现此效果~

下面附上修改后的样式：

```css
.container {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.content {
  overflow: auto;
  overflow-x: visible;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 80px;
  left: 0;
}
.fixBox {
  position: absolute;
  bottom: 0;
  height: 45px;
  width: 100%;
}
```

完结~
<br/>
