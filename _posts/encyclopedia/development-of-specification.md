---
title: 开发规范
tags:
  - 开发规范
categories:
  - 百科全书
date: 2018-11-06 20:07:42
---

## 前言

一个软件的生命周期中，80%的花费在于维护。几乎没有任何一个软件，在其整个生命同期中，均由最初的开发人员来维护。

## 规范目的

改善软件的可读性、提高代码质量、确保代码的高可维护性。包括但不限于各类资源文件的定义、命名规则、代码规范。侧重于技术要求，所有开发人员在实际开发及维护中必须严格遵守。各模块组长有责任督小组成员遵从规范，并定期做抽查，确保模块质量。对于不符合规范的代码，责令相关开发人员改正。

## 格式规范

- 安装好 IDE（vscode），需要安装对应的插件，setting 文件的配置，具体看开发快速上手文档。
- TAB 键用两个空格代替（WINDOWS 下 TAB 键占四个空格，LINUX 下 TAB 键占八个空格）。
- 文件内容编码均统一为 UTF-8。

## 命名规范

遵循以下规则

1. 有意义的名词、简短、具有可读性
2. 以小写开头 camelCase (小驼峰式命名)
3. 公共组件命名以公司名称简拼为命名空间(yht-xx.vue)，后续升级为组件库形式
4. 文件夹命名主要以功能模块代表命名 camelCase (小驼峰式命名)

> 同时还需要注意：必须符合自定义元素规范: 使用连字符分隔单词，切勿使用保留字。yht- 前缀作为命名空间: 如果非常通用的话可使用一个单词来命名，这样可以方便于其它项目里复用。

<!-- more -->

## 结构化规范

### 框架目录结构

我们已经为你生成了一个完整的开发框架，提供了涵盖中后台开发的各类功能和坑位，下面是整个项目的目录结构。

```bash
├── build                      // 构建相关
├── config                     // 配置相关
├── src                        // 源代码
│   ├── api                    // 所有请求
│   ├── assets                 // 本地静态资源
│   ├── components             // 通用组件
│   ├── directive              // 全局指令
│   ├── filters                // 全局 filter
│   ├── icons                  // 项目所有 svg icons
│   ├── lang                   // 国际化 language
│   ├── router                 // 路由
│   ├── store                  // 全局store管理
│   ├── styles                 // 全局样式
│   ├── utils                  // 工具库
│   ├── vendor                 // 公用vendor
│   ├── views                  // 业务组件
│   ├── main.js                // 入口 加载组件 初始化等
│   └── permission.js          // 权限管理
├── static                     // 第三方不打包资源
│   └── Tinymce                // 富文本
├── .babelrc                   // babel-loader 配置
├── eslintrc.js                // eslint 配置项
├── .gitignore                 // git 忽略项
├── favicon.ico                // favicon图标
├── index.html                 // html模板
└── package.json               // package.json
```

### .vue 文件基本结构

单文件组件应该总是让 `<template>` 、`<script>` 和 `<style>`标签的顺序保持一致。且 `<style>` 要放在最后，因为另外两个标签至少要有一个。

```html
<template>
  <div>
  <!--必须在div中编写页面-->
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {};
  },
  methods: {},
  mounted() {}
};
</script>
<!--声明语言，并且添加scoped-->
<style lang="less" scoped>
</style>
```

> 一个重要的事情值得注意，关注点分离不等于文件类型分离。在现代 UI 开发中，我们已经发现相比于把代码库分离成三个大的层次并将其相互交织起来，把它们划分为松散耦合的组件再将其组合起来更合理一些。在一个组件里，其模板、逻辑和样式是内部耦合的，并且把他们搭配在一起实际上使得组件更加内聚且更可维护。
>
> 即便你不喜欢单文件组件，你仍然可以把 JavaScript、CSS 分离成独立的文件然后做到热重载和预编译。

```html
<!-- my-component.vue -->
<template>
  <div>This will be pre-compiled</div>
</template>
<script src="./my-component.js"></script>
<style src="./my-component.css"></style>
```

### .vue 文件方法声明顺序(建议)

```bash
- components
- props
- data
- created
- mounted
- activited
- update
- beforeRouteUpdate
- metods
- filter
- computed
- watch
```

## 注释规范

代码注释在一个项目的后期维护中显的尤为重要，所以我们要为每一个被复用的组件编写组件使用说明，为组件中每一个方法编写方法说明。

以下情况，务必添加注释

1. 公共组件使用说明
2. 各组件中重要函数或者类说明
3. 复杂的业务逻辑处理说明
4. 特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的 hack、使用了某种算法或思路等需要进行注释描述
5. 注释块必须以 /\*\*（至少两个星号）开头\*\*/；
6. 单行注释使用 //；

### 单行注释

```js
普通方法一般使用单行注释; // 来说明该方法主要作用
```

### 多行注释

```js
// 组件使用说明，和调用说明
/**
 * 组件名称
 * @module 组件存放位置
 * @desc 组件描述
 * @author 组件作者
 * @date 2018年11月06日17:22:43
 * @param {Object} [title]    - 参数说明
 * @param {String} [columns]  - 参数说明
 * @example 调用示例
 * <yht-table :title="title" :columns="columns" :tableData="tableData"></yht-table>
 **/
```

## 编码规范

优秀的项目源码，即使是多人开发，看代码也如出一人之手。统一的编码规范，可使代码更易于阅读，易于理解，易于维护。尽量按照 **ESLint** 格式要求编写代码

1. 使用 ES6 风格编码源码

   - 坚持使用大写驼峰命名法来命名类。

     ```javascript
     // 正例
     export class ExceptionService {
       constructor() {}
     }
     // 反例
     export class exceptionService {
       constructor() {}
     }
     ```

   - 定义变量使用 let，定义常量使用 const
   - 使用 export，import 模块化

2. 组件 props 定义应该尽量详细

   - 提供默认值
   - 使用 type 属性校验类型
   - 使用 props 之前先检查该 prop 是否存在

3. 谨慎使用 this.$refs

4. 为 v-for 设置键值，总是用 key 配合 v-for。

5. 调试信息 console.log() debugger 使用完及时删除

6. 模板中的组件名使用 kebab-case (短横线分隔命名)

   ```html
   <!--正例-->
   <my-component></my-component> <!--使用 kebab-case (短横线分隔命名)-->

   <!--反例-->
   <mycomponent></mycomponent>
   <myComponent></myComponent>
   <MyComponent></MyComponent>
   ```

7. 多个属性的元素
   多个属性的元素应该分多行撰写，每个属性一行。（可在 vscode 中直接配置）

   ```html
   <!--正例-->
   <img
     src="[https://vuejs.org/images/logo.png](https://vuejs.org/images/logo.png)"
     alt="Vue Logo"
   >
   <my-component
     foo="a"
     bar="b"
     baz="c"
   ></my-component>

   <!--反例-->
   <img src="[https://vuejs.org/images/logo.png](https://vuejs.org/images/logo.png)" alt="Vue Logo">
   <my-component foo="a"  bar="b" baz="c"></my-component>
   ```

8. 指令缩写
   都用指令缩写 (用 : 表示 v-bind: 和用 @ 表示 v-on:)

   ```javascript
   // 正例
   <input
   @input="onInput"
   @focus="onFocus"
   >

   // 反例
   <input
   v-bind:value="newTodoText"
   :placeholder="newTodoInstructions"
   >
   ```

9. 样式
   所有全局样式都在 @/src/styles 目录下设置

   ```bush
   ├── styles
   │   ├── btn.scss                 # 按钮样式
   │   ├── element-ui.scss          # 全局自定义 element-ui 样式
   │   ├── index.scss               # 全局通用样式
   │   ├── mixin.scss               # 全局mixin
   │   ├── sidebar.scss             # sidebar css
   │   ├── transition.scss          # vue transition 动画
   │   └── variables.scss           # 全局变量
   ```

   常见的工作流程是，全局样式都写在 src/styles 目录下，每个页面自己对应的样式都写在自己的 .vue 文件之中

   ```css
   <style>
   /* global styles */
   </style>

   <style scoped>
   /* local styles */
   </style>
   ```
