---
title: 用 CSS/CSS3 实现水平居中和垂直居中
tags:
  - Css/Css3
  - Html
categories:
  - 技术渣
date: 2018-09-14 10:41:03
---

## 水平居中

### 行内元素

只需要把行内元素包裹在一个属性 `display` 为 `block` 的父层元素中，并且把父层元素添加如下属性

```css
.parent {
  text-align: center;
}
```

### 块状元素

```css
.item {
  /* 这里可以设置顶端外边距 */
  margin: 10px auto;
}
```

### 多个块状元素

将元素的 `display` 属性设置为 `inline-block`，并且把父元素的 `text-align` 属性设置为 `center`

```css
.parent {
  text-align: center;
}
```

### 多个块状元素 (使用 flexbox 布局实现)

使用 `flexbox`，只需要把待处理的块状元素的父元素添加属性 `display:flex` 及 `justify-content:center`

```css
.parent {
  display: flex;
  justify-content: center;
}
```

## 垂直居中

### 单行的行内元素

```css
.parent {
  background: #222;
  height: 200px;
}

/* 以下代码中，将a元素的height和line-height设置的和父元素一样高度即可实现垂直居中 */
.parent a {
  height: 200px;
  line-height: 200px;
  color: #fff;
}
```

### 多行的行内元素

组合使用 `display:table-cell` 和 `vertical-align:middle` 属性来定义需要居中的元素的父容器元素生成效果

```css
.parent {
  background: #222;
  width: 300px;
  height: 300px;
  /* 以下属性垂直居中 */
  display: table-cell;
  vertical-align: middle;
}
```

### 已知高度的块状元素

```css
.item {
  top: 50%;
  margin-top: -50px; /* margin-top值为自身高度的一半 */
  position: absolute;
  padding: 0;
}
```

## 水平垂直居中

### 已知高度和宽度的元素

#### 方案 1

这是一种不常见的居中方法，可自适应，比方案 2 更智能，如下

```css
.item {
  position: absolute;
  margin: auto;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
}
```

#### 方案 2

```css
.item {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -75px; /* 设置margin-left / margin-top 为自身高度的一半 */
  margin-left: -75px;
}
```

### 未知高度和宽度元素

```css
.item {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* 使用css3的transform来实现 */
}
```

### 使用 flex 布局实现

```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
  /* 注意这里需要设置高度来查看垂直居中效果 */
  background: #aaa;
  height: 300px;
}
```
