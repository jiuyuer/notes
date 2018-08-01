---
title: JavaScript跳出循环的方法及区别
tags:
  - JavaScript
categories:
  - 技术渣
date: 2018-08-01 17:25:22
---

跟许多多态语言一样，js 也有 break，continue，return

面向对象编程语法中我们会碰到 break，continue，return 这三个常用的关键字，那么关于这三个关键字的使用具体的操作是什么呢？我们在使用这三关键字的时候需要注意和需要理解的规则是什么呢？让我们开始介绍吧

## js 编程语法之 break 语句

break 语句会使运行的程序立刻退出包含在最内层的循环或者退出一个 switch 语句。

由于它是用来退出循环或者 switch 语句，所以只有当它出现在这些语句时，这种形式的 break 语句才是合法的。

如果一个循环的终止条件非常复杂，那么使用 break 语句来实现某些条件比用一个循环表达式来表达所有的条件容易得多。

```javascript
for (var i = 1; i <= 10; i++) {
  if (i == 8) {
    break;
  }
  document.write(i);
}
```

当 i=8 的时候，直接退出 for 这个循环。这个循环将不再被执行！

//输出结果：1234567

## js 编程语法之 continue 语句

continue 语句和 break 语句相似。所不同的是，它不是退出一个循环，而是开始循环的一次新迭代。

continue 语句只能用在 while 语句、do/while 语句、for 语句、或者 for/in 语句的循环体内，在其它地方使用都会引起错误！

```javascript
for (var i = 1; i <= 10; i++) {
  if (i == 8) {
    continue;
  }
  document.write(i);
}
```

当 i=8 的时候，直接跳出本次 for 循环。下次继续执行。

//输出结果：1234567910

## js 编程语法之 return 语句

return 语句就是用于指定函数返回的值。return 语句只能出现在函数体内，出现在代码中的其他任何地方都会造成语法错误！

```javascript
for (var i = 1; i <= 10; i++) {
  if (i == 8) {
    return;
  }
  document.write(i);
}
```

执行结果 Uncaught SyntaxError: Illegal return statement(…)
意思是非法捕获的查询返回语句。

当执行 return 语句时，即使函数主体中还有其他语句，函数执行也会停止！

```javascript
if (username == '') {
  alert('请输入用户名');
  return false;
}
if (qq == '') {
  alert('请输入QQ');
  return false;
}
```

上面的实例里，当 username 为空时，就不会再向下执行

<br/>
