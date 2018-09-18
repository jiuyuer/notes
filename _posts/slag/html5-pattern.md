---
title: 一些有用的 HTML5 pattern
tags:
  - HTML5
  - 数字键盘
categories:
  - 技术渣
date: 2018-09-18 11:45:02
---

最近在做手机页面时，遇到数字输入的键盘的问题，之前的做法只是一刀切的使用 `type="tel"`，不过一直觉得九宫格的电话号码键盘上的英文字母太碍事了。于是想要尝试其它的实现方案，最终的结论却令人沮丧。不过也趁机详细了解了下 `pattern` 这个属性。

## `type="tel"` 和 `type="number"` 的区别

这里还是先那么先交代一下最初遇到的问题。其实无论是 tel 还是 number 都不是完美的：

### type="tel"

- 优点是 iOS 和 Android 的键盘表现都差不多
- 缺点是那些字母好多余，虽然我没有强迫症但还是感觉怪怪的啊。

### type="number"

- 优点是 Android 下实现的一个真正的数字键盘
- 缺点一：iOS 下不是九宫格键盘，输入不方便
- 缺点二：旧版 Android（包括微信所用的 X5 内核）在输入框后面会有超级鸡肋的小尾巴，好在 Android 4.4.4 以后给去掉了。

<!-- more -->

不过对于缺点二，我们可以用 webkit 私有的伪元素给 fix 掉：

```css
input[type='number']::-webkit-inner-spin-button,
input[type='number']::-webkit-outer-spin-button {
  -webkit-appearance: none;
  appearance: none;
  margin: 0;
}
```

## pattern 属性

pattern 用于验证表单输入的内容，通常 HTML5 的 type 属性，比如 email、tel、number、data 类、url 等，已经自带了简单的数据格式验证功能了，加上 pattern 后，前端部分的验证更加简单高效了。

显而易见，pattern 的属性值要用正则表达式。

实例

简单的数字验证

数字的验证有两个：

```html
<input type="number" pattern="\d">
<input type="number" pattern="[0-9]*">
```

对表单验证来说，这两个正则的作用是一样的，表现的话差异就很大：

- iOS 中，只有[0-9]\*才可以调起九宫格数字键盘，\d 无效
- Android 4.4 以下(包括 X5 内核)，两者都调起数字键盘；
- Android 4.4.4 以上，只认 type 属性，也就是说，如果上面的代码将 type="number" 改为 type="text" ，将调起全键盘而不会是九宫格数字键盘。

## 常用的正则表达式

pattern 的用法都一样，这里不再啰嗦各种详细写法了，只是列出来一些常用的正则就好了：

- 信用卡 [0-9]{13,16}
- 银联卡 ^62[0-5]\d{13,16}$
- Visa: ^4[0-9]{12}(?:[0-9]{3})?$
- 万事达：^5[1-5][0-9]{14}$
- QQ 号码：[1-9][0-9]{4,14}
- 手机号码：^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$
- 身份证：^([0-9]){7,18}(x|X)?$
- 密码：^[a-zA-Z]\w{5,17}$ 字母开头，长度在 6~18 之间，只能包含字母、数字和下划线
- 强密码：^(?=.\d)(?=.[a-z])(?=.\*[A-Z]).{8,10}$ 包含大小写字母和数字的组合，不能使用特殊字符，长度在 8-10 之间
- 7 个汉字或 14 个字符：^[\u4e00-\u9fa5]{1,7}$|^[\dA-Za-z_]{1,14}$

## 浏览器支持

很不幸，pattern 的浏览器支持很惨： via [Can I Use](http://caniuse.com/#feat=input-pattern)

但是如果只是如文章开头提到的改数字键盘的话，iOS 和 Android 都是没有问题的。

<br/>

转自：https://www.qianduan.net/xie-you-yong-de-html5-pattern/
