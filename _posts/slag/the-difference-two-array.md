---
title: 求两数组的difference
tags:
  - JavaScript
categories:
  - 技术渣
date: 2018-06-08 16:35:00
---

### 需求

```javascript
var arr1 = [1, 2, 2, 3, 4, 5];
var arr2 = [1, 2];
求两数据的不同值，结果为[3, 4, 5]
```

### 方案一

调用第三方工具：underscore

```javascript
var arr1 = [1, 2, 2, 3, 4, 5];
var arr2 = [1, 2];
_.difference(arr1, arr2);
=> [3, 4, 5]
```

### 方案二

手写常规办法，创建临时数组

```javascript
// past
var arr1 = [1, 2, 2, 3, 4, 5];
var arr2 = [1, 2];
var temp = [];
for (var i = 0; i < arr1.length; i++) {
  if (arr2.indexOf(arr1[i]) === -1) {
    temp.push(arr1[i]);
  }
}
console.log(temp);
```

### 方案三

调用 es6 的数组操作 api

```javascript
// es6
let arr1 = [1, 2, 2, 3, 4, 5];
let arr2 = [1, 2];
console.log(arr1.filter(item => !arr2.includes(item)));
```

就酱~
<br>
