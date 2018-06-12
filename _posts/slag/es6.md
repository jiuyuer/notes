---
title: ES6常用方法
tags:
  - Javascript
  - ES6
categories:
  - 技术渣
date: 2018-06-12 09:07:27
---

## let 命令 和 const 命令

### let 命令：

let 用于声明变量，但是所有声明的变量只在 let 命令所在的代码块有效。
let 不允许在同以作用域中重复声明变量。
let 不存在变量提升，所以变量一定要在声明后使用，否则会报错。

### const 命令:

const 命令用来声明常量，一旦声明，其值就不能改变，即 const 一旦声明常量就必须立刻初始化，不能留到以后赋值。
const 命令只是保证变量名指向的地址不变，并步保证该地址的数据不变。

### 相同点：

let 和 const 命令声明的变量都只在它们所在的块级作用域中才有效。
如果区块中存在 let 和 const 命令，则这个区块对这些命令声明的变量从一开始就形成封闭作用域。

## 变量的结构赋值

ES6 允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，称为解构。

### 数组

```javascript
let [a, b, c,d] = [“aa”, “bb”, 77,88];  //数组结构
let [a,b,[c,d],e] =[“aa”,’bb’,[33,44],55];  //嵌套数组解构
let [a,b,,e] =[“aa”,’bb’,[33,44],55]; //空缺变量
let [a,b,,e,f] =[“aa”,’bb’,[33,44],55]; //多余变量
let [a,b,,e,f=’hello’] =[“aa”,’bb’,[33,44],55]; //默认值
```

### 对象解构

```javascript
let obj = { uid: 121, uname: '张三' };
let obj = new Object();
obj.uid = 111;
obj.uname = '张三';
let { uid: id, uname: name } = obj; //顺序改变无影响
console.log(name); //张三

//小括号：
let uid, uname;
({ uid, uname } = obj); //必须有小括号，否则{}就会被解读为语句块
console.log(uname); //张三

//  PS: 可嵌套 ，可有默认值
```

### 字符串解构

```javascript
let [a, b, c, d] = '倚天屠龙';
console.log(a, b, c, d);
```

### 函数参数解构

```javascript
let obj = { uid: 121, uname: '张三' };
function analysis({ uid, uname }) {
  console.log(uid);
  console.log(uname);
}

//-------以下也正确
function analysis({ uname }) {
  console.log(uname);
}

analysis(obj);

//  PS: 参数中数组、字符串、默认值、缺位均支持 。
```

## [数组操作 Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

### forEach()

方法对数组的每个元素执行一次提供的函数。

```javascript
let array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

### filter()

方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```javascript
let words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);
console.log(result);

// expected output: Array ["exuberant", "destruction", "present"]
```

### map()

方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```javascript
// ES6
let numbers = [1, 5, 10, 15];
let doubles = numbers.map(x => x ** 2);

// doubles is now [1, 25, 100, 225]
// numbers is still [1, 5, 10, 15]

const numbers = [2, 4, 8, 10];
let halves = numbers.map(x => x / 2);

let numbers = [1, 4, 9];
let roots = numbers.map(Math.sqrt);

// roots is now [1, 2, 3]
// numbers is still [1, 4, 9]
```

### includes()

方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。

```javascript
let array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

let pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
```

## [箭头函数表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

语法比函数表达式更短，并且没有自己的 this，arguments，super 或 new.target。这些函数表达式更适用于那些本来需要匿名函数的地方，并且它们不能用作构造函数。

```javascript
var materials = ['Hydrogen', 'Helium', 'Lithium', 'Beryllium'];

materials.map(function(material) {
  return material.length;
}); // [8, 6, 7, 9]

materials.map(material => {
  return material.length;
}); // [8, 6, 7, 9]

materials.map(material => material.length); // [8, 6, 7, 9]
```

## [import](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import)

import 语句用于导入由另一个模块导出的绑定。无论是否声明了 strict mode ，导入的模块都运行在严格模式下。import 语句不能在嵌入式脚本中使用。

```javascript
import defaultExport from "module-name";
import * as name from "module-name";
import { export } from "module-name";
import { export as alias } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
```

> defaultExport

- 将引用模块默认导出的名称。

> module-name

- 要导入的模块。这通常是包含模块的.js 文件的相对或绝对路径名，不包括.js 扩展名。某些打包工具可以允许或要求使用该扩展；检查你的运行环境。只允许单引号和双引号的字符串。

> name

- 引用时将用作一种命名空间的模块对象的名称。

> export, exportN

- 要导入的导出名称。

> alias, aliasN

- 将引用指定的导入的名称。

## [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

### [Promise 对象](http://es6.ruanyifeng.com/#docs/promise)

- Promise 的含义
- 基本用法
- Promise.prototype.then()
- Promise.prototype.catch()
- Promise.prototype.finally()
- Promise.all()
- Promise.race()
- Promise.resolve()
- Promise.reject()
- 应用
- Promise.try()

## Sass/Less/PostCSS

### [Sass](https://www.sass.hk)

世界上最成熟、最稳定、最强大的专业级 CSS 扩展语言！

### [Less](http://www.bootcss.com/p/lesscss/)

一种 动态 样式 语言.
LESS 将 CSS 赋予了动态语言的特性，如 变量， 继承， 运算， 函数. LESS 既可以在 客户端 上运行 (支持 IE 6+, Webkit, Firefox)，也可以借助 Node.js 或者 Rhino 在服务端运行。
