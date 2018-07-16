---
title: 培训文档（基于Vue2.0的项目开发）
tags:
  - JavaScript
  - 培训文档
  - Vue.js
categories:
  - 百科全书
date: 2018-06-18 19:01:31
---

注：[Vue2.0 中文文档](https://cn.vuejs.org) ，如果对自己英文有信心，也可以直接阅读 [英文文档](https://vuejs.org)。

## 起步：从了解 Vue 开始

1.  扎实的 JavaScript / HTML / CSS 基本功。这是前置条件。

2.  通读官方教程 (guide) 的基础篇。不要用任何构建工具，就只用最简单的 &lt;script&gt;，把教程里的例子模仿一遍，理解用法。<strong>不推荐上来就直接用 vue-cli 构建项目，尤其是如果没有 Node/Webpack 基础。</strong>

3.  照着官网上的示例，自己想一些类似的例子，模仿着实现来练手，加深理解。

4.  阅读官方教程进阶篇的前半部分，到『自定义指令 (Custom Directive) 』为止。着重理解 Vue 的响应式机制和组件生命周期。『渲染函数（Render Function)』如果理解吃力可以先跳过。

5.  阅读教程里关于路由和状态管理的章节，然后根据需要学习 vue-router 和 vuex。同样的，先不要管构建工具，以跟着文档里的例子理解用法为主。

6.  走完基础文档后，如果你对于基于 Node 的前端工程化不熟悉，就需要补课了。下面这些严格来说并不是 Vue 本身的内容，也不涵盖所有的前端工程化知识，但对于大型的 Vue 工程是前置条件，也是合格的『前端工程师』应当具备的知识。

## 前端生态/工程化

1.  了解 JavaScript 背后的规范，ECMAScript 的历史和目前的规范制定方式。学习 ES2015/16 的新特性，理解 ES2015 modules，适当关注[还未成为标准的提案](https://github.com/tc39/proposals)。

2.  学习命令行的使用。建议用 Mac。

3.  学习 Node.js 基础。<strong>建议使用 [nvm](https://github.com/creationix/nvm) 这样的工具来管理机器上的 Node 版本，并且将 npm 的 registry 注册表配置为[淘宝的镜像源](https://npm.taobao.org)。</strong>至少要了解 npm 的常用命令，npm scripts 如何使用，语义化版本号规则，CommonJS 模块规范（了解它和 ES2015 Modules 的异同），Node 包的解析规则，以及 Node 的常用 API。应当做到可以自己写一些基本的命令行程序。注意最新版本的 Node (6+) 已经支持绝大部分 ES2015 的特性，可以借此巩固 ES2015。

4.  了解如何使用 / 配置 Babel 来将 ES2015 编译到 ES5 用于浏览器环境。

5.  学习 Webpack。Webpack 是一个极其强大同时也复杂的工具，作为起步，理解它的『一切皆模块』的思想，并基本了解其常用配置选项和 loader 的概念/使用方法即可，比如如何搭配 Webpack 使用 Babel。学习 Webpack 的一个挑战在于其本身文档的混乱，建议多搜索搜索，应该还是有质量不错的第三方教程的。英文好的建议阅读 [Webpack 2.0 的文档](https://webpack.js.org/guides/getting-started/)。

<!-- more -->
## Vue 进阶

1.  有了 Node 和 Webpack 的基础，可以通过 vue-cli 来搭建基于 Webpack ，并且支持单文件组件的项目了。建议用 webpack-simple 这个模板开始，并阅读官方教程进阶篇剩余的内容以及 [vue-loader 的文档](https://vue-loader.vuejs.org)，了解一些进阶配置。有兴趣的可以自己亲手从零开始搭一个项目加深理解。

2.  根据 [例子](https://github.com/vuejs/vue-hackernews-2.0) 尝试在 Webpack 模板基础上整合 [Vue-router](https://vue-loader.vuejs.org/zh/guide/) 和 [Vuex](https://vuex.vuejs.org/zh/)

3.  深入理解 Virtual DOM 和『渲染函数 (Render Functions)』这一章节（可选择性使用 JSX)，理解模板和渲染函数之间的对应关系，了解其使用方法和适用场景。

4.  （可选）根据需求，了解服务端渲染的使用（需要配合 Node 服务器开发的知识）。其实更重要的是理解它所解决的问题并搞清楚你是否需要它。

5.  阅读开源的 Vue 应用、组件、插件源码，自己尝试编写开源的 Vue 组件、插件。

6.  参考 [贡献指南](https://github.com/vuejs/vue/blob/dev/.github/CONTRIBUTING.md#development-setup) 阅读 Vue 的源码，理解内部实现细节。（需要了解 [Flow](https://flow.org)）

## 了解 ES6

推荐阮一峰老师的 [ECMAScript 6 入门](http://es6.ruanyifeng.com/#README)

重点学习：

- let 和 const 命令
- 变量的解构赋值
- 箭头函数表达式
- Module 的语法
- Promise 对象

## Sass/Less/PostCSS ...

[Sass](https://www.sass.hk)

世界上最成熟、最稳定、最强大的专业级 CSS 扩展语言！

[Less](http://www.bootcss.com/p/lesscss/)

一种 动态 样式 语言.
LESS 将 CSS 赋予了动态语言的特性，如 变量， 继承， 运算， 函数. LESS 既可以在 客户端 上运行 (支持 IE 6+, Webkit, Firefox)，也可以借助 Node.js 或者 Rhino 在服务端运行。

[PostCSS](https://segmentfault.com/a/1190000011595620)
...

## NPM

会一些 npm 基础，知道如何用 git-bash 来安装依赖，会一些常用的命令。

这方面的知识可以参阅 [npm 入门文档](https://segmentfault.com/a/1190000005799797)

- npm install [package][—save] [—saveDev]
- npm update
- npm uninstall <package>
- npm start
- npm run <scripts>

## 项目管理相关

### [Git](https://git-scm.com)

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
GIT 不仅仅是个版本控制系统，它也是个内容管理系统(CMS)，工作管理系统等。
如果你是一个具有使用 SVN 背景的人，你需要做一定的思想转换，来适应 GIT 提供的一些概念和特征。

Git 与 SVN 区别点：

1.  GIT 是分布式的，SVN 不是：这是 GIT 和其它非分布式的版本控制系统，例如 SVN，CVS 等，最核心的区别。
2.  GIT 把内容按元数据方式存储，而 SVN 是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn,.cvs 等的文件夹里。
3.  GIT 分支和 SVN 的分支不同：分支在 SVN 中一点不特别，就是版本库中的另外的一个目录。
4.  GIT 没有一个全局的版本号，而 SVN 有：目前为止这是跟 SVN 相比 GIT 缺少的最大的一个特征。
5.  GIT 的内容完整性要优于 SVN：GIT 的内容存储使用的是 SHA-1 哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。

Git 完整命令手册地址：http://git-scm.com/docs

### 接口文档（API 文档）

随着互联网技术的发展，现在的网站架构基本都由原来的后端渲染，变成了：前端渲染、后端分离的形态，而且前端技术和后端技术在各自的道路上越走越远。
前端和后端的唯一联系，变成了 API 接口；API 文档变成了前后端开发人员联系的纽带，变得越来越重要

#### API 文档工具

- [RAP](http://rapapi.org/org/index.do)
RAP 是一个可视化接口管理工具 通过分析接口结构，动态生成模拟数据，校验真实接口正确性， 围绕接口定义，通过一系列自动化工具提升我们的协作效率。我们的口号：提高效率，回家吃晚饭！

- [Swaggger](https://swagger.io)（推荐）
The Best APIs are Built with Swagger Tools

- [小幺鸡](http://www.xiaoyaoji.cn)
小幺鸡，简单好用的在线接口文档管理工具

### 数据 Mock

[Easy-Mock](https://www.easy-mock.com)
是一个  可视化，并且能快速生成模拟数据的服务。

## 框架介绍

### 目录结构

```bash
├── build                      // 构建相关  
├── config                     // 配置相关
├── src                        // 源代码
│   ├── api                    // 所有请求统一调用并管理
│   ├── assets                 // 主题 字体等静态资源
│   ├── components             // 全局公用组件
│   ├── filters                // 全局 filter
│   ├── router                 // 路由
│   ├── store                  // 全局 store管理
│   ├── styles                 // 全局样式
│   ├── utils                  // 全局公用方法
│   ├── views                  // 路由页面组件
│   ├── main.js                // 入口 加载组件 初始化等
├── static                     // 第三方不打包资源
├── .babelrc                   // babel-loader 配置
├── .eslintrc.js               // eslint 配置项
├── .gitignore                 // git 忽略项
├── favicon.ico                // favicon图标
├── index.html                 // html模板
└── package.json               // package.json
```

### 安装

```bash
# install dependencies
npm install

# serve with hot reload at localhost:9525
npm run dev

# build for production with minification
npm run build
```

强烈建议不要用直接使用 cnpm 安装有各种诡异的 bug，可以通过重新指定 registry 来解决 npm 安装速度慢的问题，如下：

```bash
npm install --registry=https://registry.npm.taobao.org
```

## 引入第三方库

### [VUX](https://doc.vux.li/zh-CN/)

VUX（读音 [v’ju:z]，同 views）是基于 WeUI 和 Vue(2.x)开发的移动端 UI 组件库，主要服务于微信页面。

组件地址：https://doc.vux.li/zh-CN/components/actionsheet.html
DEMO 地址：https://vux.li/demos/v2/

### [WeUI](https://github.com/Tencent/weui/blob/master/README_cn.md)

WeUI 是一套同微信原生视觉体验一致的基础样式库，由微信官方设计团队为微信 Web 开发量身设计，可以令用户的使用感知更加统一。包含 button、cell、dialog、 progress、 toast、article、actionsheet、icon 等各式元素。

DEMO 地址：https://weui.io
