---
title: 由对象组成的数组如何去重？
tags:
  - JavaScript
categories:
  - 技术渣
date: 2018-10-08 16:13:41
---

需求：将下面 data 数组中 id 重复的数据去掉？

```javascript
let data = [
  { id: 201801, name: '张三', age: 15 },
  { id: 201804, name: 'John', age: 18 },
  { id: 201802, name: '李四', age: 18 },
  { id: 201801, name: '张三', age: 15 },
  { id: 201805, name: 'Jack', age: 18 },
  { id: 201803, name: '王五', age: 10 },
  { id: 201805, name: 'Jack', age: 18 },
  { id: 201804, name: 'John', age: 18 },
  { id: 201805, name: 'Jack', age: 18 }
];
```

下面列了两种办法来解决：

## 一、数组的 reduce()方法

```javascript
let hash = {};
data = data.reduce((preVal, curVal) => {
  hash[curVal.id] ? '' : (hash[curVal.id] = true && preVal.push(curVal));
  return preVal;
}, []);
```

### 上述方法的实现思路

利用 [reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)方法的累积器作用，在对由对象组成的数组进行遍历时，通过对象 `hash` 来标记数组中每个元素 id 是否出现过，如果出现过，那么遍历到的当前元素则不会放入到累积器中，如果没有出现，则添加到累积器中，这样保证了最后返回值中每个数据 id 的唯一性。

关于数组的 reduce()方法，[点这里](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)，MDN 上已经写的很清楚了，自己理解。

## 二、for 循环遍历

```javascript
function removeRepeat(arr, key) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i][key] === arr[j][key]) {
        arr.splice(j, 1);
        j = j - 1; // 关键，因为splice()删除元素之后，会使得数组长度减小，此时如果没有j=j-1的话，会导致相同id项在重复两次以上之后无法进行去重，且会错误删除id没有重复的项。
      }
    }
  }
}
removeRepeat(data, 'id');
```

### 上述方法的实现思路

利用 for 循环遍历数组，并将数组中的每一个元素与剩余元素一一进行比较，如果在剩余元素中出现 id 相同的项，则通过 `splice()`方法将相同 id 项删除，这样在最终得到的数组中每个数据 id 将是唯一的。通过 `splice()`方法删除元素后，会使得数组长度减小，为了实现去重应该执行 `j = j-1`。上面将去重方法直接封装成函数 `removeRepeat`，使用时可以直接调用该函数，并传入要去重的数组和唯一属性名。

<br/>

转自 https://blog.csdn.net/XuM222222/article/details/80657316
