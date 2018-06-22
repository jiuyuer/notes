---
title: 关于Chrome警告： Unable to preventDefault inside passive event listener 的解决方案
tags:
  - JavaScript
  - FastClick
  - 移动端
categories:
  - 技术渣
date: 2018-06-22 10:53:26
---

最近在移动端 H5 项目开发中，经常在 chrome 的控制台看到如下提示：

```bush
[Intervention] Unable to preventDefault inside passive event listener due to target being treated as passive. See https://www.chromestatus.com/features/5093566007214080
```

首先，之所以报错是因为引入了 FastClick（为了解决 300ms 的 click 延迟）

于是 Google 了一番，找到这篇文章，有了详细解释
https://developers.google.cn/web/updates/2017/01/scrolling-intervention

简而言之：

> 由于浏览器必须要在执行事件处理函数之后，才能知道有没有掉用过 preventDefault() ，这就导致了浏览器不能及时响应滚动，略有延迟。

> 所以为了让页面滚动的效果如丝般顺滑，从 chrome56 开始，在 window、document 和 body 上注册的 touchstart 和 touchmove 事件处理函数，会默认为是 passive: true。浏览器忽略 preventDefault() 就可以第一时间滚动了。

举例：

```javascript
wnidow.addEventListener('touchmove', func) 效果和下面一句一样
wnidow.addEventListener('touchmove', func, { passive: true })
```

这就导致了一个问题：

> 如果在以上这 3 个元素的 touchstart 和 touchmove 事件处理函数中调用 e.preventDefault() ，会被浏览器忽略掉，并不会阻止默认行为。

测试：

```javascript
body {
  margin: 0;
  height: 2000px;
  background: linear-gradient(to bottom, red, green);
}

// 在 chrome56 中，照样滚动，而且控制台会有提示，blablabla
window.addEventListener('touchmove', e => e.preventDefault())
```

<!-- more -->

那么如何解决这个问题呢？不让控制台提示，而且 preventDefault() 有效果呢？

两个方案：

1.  注册处理函数时，用如下方式，明确声明为不是被动的

    ```javascript
    window.addEventListener('touchmove', func, { passive: false })
    ```

    在 touch 的事件监听方法上绑定第三个参数{ passive: false }，通过传递 passive 为 false 来明确告诉浏览器：事件处理程序调用 preventDefault 来阻止默认滑动行为。

2.  应用 CSS 属性 touch-action: none; 这样任何触摸事件都不会产生默认行为，但是 touch 事件照样触发。
    touch-action 还有很多选项，详细请参考 [touch-action](https://w3c.github.io/pointerevents/#the-touch-action-css-property);

**Passive event listeners**

2016 年 Google I/O 上提出的概念，目的是用来提升页面滑动的流畅度。

> For instance, in Chrome for Android 80% of the touch events that block scrolling never actually prevent it. 10% of these events add more than 100ms of delay to the start of scrolling, and a catastrophic delay of at least 500ms occurs in 1% of scrolls.

在 Android 版 Chrome 浏览器的 touch 事件监听器的页面中，80% 的页面都不会调用 preventDefault 函数来阻止事件的默认行为。在滑动流畅度上，有 10% 的页面增加至少 100ms 的延迟，1% 的页面甚至增加 500ms 以上的延迟。

由于浏览器无法预先知道一个事件处理函数中会不会调用 preventDefault()，它需要等到事件处理函数执行完后，才能去执行默认行为，然而事件处理函数执行是要耗时的，这样一来就会导致页面卡顿，也就是说，当浏览器等待执行事件的默认行为时，大部分情况是白等了。

如果 Web 开发者能够提前告诉浏览器：“我不调用 preventDefault 函数来阻止事件事件行为”，那么浏览器就能快速生成事件，从而提升页面性能，Passive event listeners 的提出就解决了这样的问题。

<br/>