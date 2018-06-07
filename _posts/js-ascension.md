---
title: js提升
tags:
  - Javascript
categories:
  - 技术渣
date: 2017-09-14 17:25:27
---

这里的提升，我的理解是包括变量和函数在内的所有声明的提升
而根据对作用域的理解，任何声明在某个作用域内的变量，都将附属于这个作用域。

## 考虑以下代码

```javascript
//代码块一
a = 2;
var a;
console.log(a);

//代码块二
console.log(a);
var a = 2;
```

上述两段代码的结果是啥？

思考思路：包括变量和函数在内的所有声明都会在任何代码被执行前首先被处理。

## 变量声明

于是， 上述代码块一，会以如下形式处理：

```javascript
var a;
a = 2;
console.log(a);
```

代码块二处理：

```javascript
var a;
console.log(a);
a = 2;
```

## 函数声明

```javascript
foo();
function foo() {
  console.log(a); //undefined
  var a = 2;
}
```

<!-- more -->

上述代码理解为下面的形式：

```javascript
function foo() {
  var a;
  console.log(a); //undefined
  a = 2;
}
foo();
```

> 提示：函数声明会被提升，但是函数表达式却不会被提升

如下代码：

```javascript
foo();
//不是 ReferenceError(引用错误)，对象表明一个不存在的变量被引用
//而是 TypeError(类型错误),对象用来表示值的类型非预期类型时发生的错误
var foo = function bar() {
  // ...
};
```

可以理解为下面形式：

```javascript
var foo;
foo(); // 报TypeError错误
foo = function bar() {
  // ...
};
```

再来一道题，大家自行理解

```javascript
foo();
bar();
var foo = function bar() {
  // ...
};
```

> 提升：变量和函数声明从它们在代码中出现的位置被“移动”到了最上面的过程
> 重要提示：只有声明本身会被提升，而赋值或其他运行逻辑会留在原地。

## 函数优先

函数声明和变量声明在被提升的同时，如果在一个作用域中同时存在多个“重复”或者说同名的声明代码中，函数会首先被提升，然后才是变量。

考虑以下代码：

```javascript
foo(); // 1
var foo;
function foo() {
  console.log(1);
}
foo = function() {
  console.log(2);
};
```

可以理解为如下形式：

```javascript
function foo() {
  console.log(1);
}
foo();
foo = function() {
  console.log(2);
};
```

> 提示：出现在后面的函数声明还是可以覆盖前面的

js 语言精粹提到的糟粕中有类似的这么一段：

```javascript
foo(); // 是‘b’ 还是 TypeError: foo is not a function?
var a = true;
if (a) {
  function foo() {
    console.log('a');
  }
} else {
  function foo() {
    console.log('b');
  }
}
```

上面这段代码在 Gecko 引擎中打印”TypeError”；而在其他浏览器中则打印”b”。

原因在于 Gecko 加入了 ECMAScript 以外的一个 feature：条件式函数声明。

注意引用的 Note：条件式函数声明跟函数表达式的处理方式一样。因此，条件式函数声明丧失了函数声明提升的特性。

基于以上原因，请不要在你的代码里将函数声明嵌套在条件语句内。

写成函数表达式好了。
