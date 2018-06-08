---
title: Vue 组件间通信
tags:
  - Javascript
  - Vue2.0
categories:
  - 技术渣
date: 2017-11-13 19:57:24
---

分两种，父子组件与非父子组件的通信

## 父子组件通信

首先要明白，在 Vue 中，父子组件的关系可以总结为 prop 向下传递，事件向上传递

也就是说父组件通过 prop 给子组件下发数据，子组件通过 事件 给父组件发送消息

注：如果你想把一个对象的所有属性作为 prop 进行传递，可以使用不带任何参数的 v-bind(即用 v-bind 而不是 v-bind:prop-name)。例如，已知一个 todo 对象：

```javascript
todo: {
   text: 'Learn Vue',
   isComplete: false
}
```

然后：

```javascript
<todo-item v-bind="todo" />
```

将等价于：

```javascript
<todo-item v-bind:text="todo.text" v-bind:is-complete="todo.isComplete" />
```

通过 Vue 的自定义事件来解决子组件给父组件发送消息

每个 Vue 实例都实现了事件接口，即：

- 使用 $on(eventName) 监听事件
- 使用 $emit(eventName) 触发事件

> PS：在项目中有时也会碰到父与子孙组件的通信，这时，需要在子组件中给对应的数据添加 watch 来时时响应才行

## 非父子组件通信

有两种办法解决：

#### 一、组件间相对简单情况下

有时候，非父子关系的两个组件之间也需要通信。在简单的场景下，可以使用一个空的 Vue 实例作为事件总线：

```javascript
var bus = new Vue();
// 触发组件 A 中的事件
bus.$emit('id-selected', 1);
// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function(id) {
  // ...
});
```

这个时候，可能我们就需要定义一个全局变量来分配各个组件间的通信事件

#### 二、组件复杂的情况下

官方文档推荐考虑使用专门的状态管理模式（Vuex）。
