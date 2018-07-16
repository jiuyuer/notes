---
title: eslint 验证 no-unneeded-ternary
tags:
  - JavaScript
  - Eslint
categories:
  - 技术渣
date: 2018-06-23 17:18:59
---

项目中引入 Eslint 进行团队开发，配置好之后，报错提示如下：

```bash
 http://eslint.org/docs/rules/no-unneeded-ternary  Unnecessary use of boolean literals in conditional expression  
```

文档的意思是 **禁止不必要的嵌套**

源代码：

```javascript
this.btnStatus = this.btnStatus === true ? false : true
```

然后点开对应的链接就发现问题所在了~

**链接中的内容** (就不翻译直接引入了。。。)

> It’s a common mistake in JavaScript to use a conditional expression to select between two Boolean values instead of using ! to convert the test to a Boolean. Here are some examples:

```javascript
// Bad
var isYes = answer === 1 ? true : false

// Good
var isYes = answer === 1

// Bad
var isNo = answer === 1 ? false : true

// Good
var isNo = answer !== 1
```

> Another common mistake is using a single variable as both the conditional test and the consequent. In such cases, the logical OR can be used to provide the same functionality. Here is an example:

```javascript
// Bad
var foo = bar ? bar : 1

// Good
var foo = bar || 1
```

所以。。。

修改源代码之后的结果：

```javascript
this.btnStatus = this.btnStatus !== true
```

报错/警告 问题解决了~
<br>
