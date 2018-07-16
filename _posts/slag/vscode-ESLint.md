---
title: 使用 vscode 配置 ESLint
tags:
  - JavaScript
  - vscode
  - Eslint
categories:
  - 技术渣
date: 2018-06-25 15:55:21
---

### [Eslint](http://eslint.org)

最初是由 Nicholas C. Zakas 于 2013 年 6 月创建的开源项目。它的目标是提供一个插件化的 javascript 代码检测工具。
对于每一个开发者(尤其是团队项目开发)而言都是非常值得使用的，这样会强制你写出高质量且整洁的代码

### [VS Code](https://code.visualstudio.com)

Visual Studio Code 是一款免费开源的现代化轻量级代码编辑器，支持几乎所有主流的开发语言的语法高亮、智能代码补全、自定义热键、括号匹配、代码片段、代码对比 Diff、GIT 等特性，支持插件扩展，并针对网页开发和云端应用开发做了优化。软件跨平台支持 Win、Mac 以及 Linux。

### VUE + VSCode + Eslint

在使用 VSCode 编辑器开发 vue 项目时，当使用 vscode 自带的格式化代码，让 vue 项目的代码风格统一，整洁就很有必要了。

折腾了两天，看了好些文档，虽然总感觉并没有真正理解，但好歹也出了点成果

使用 eslint + VSCode 来写 vue 。 每次保存，vscode 就能标红不符合 eslint 规则的地方，同时还会做一些简单的自我修正

首先安装 eslint 插件，上文有官网通道，自己去官方查看安装步骤。

安装并配置完成 ESLint 后，我们继续回到 VSCode 进行扩展设置，点击 首选项 > 设置 打开 VSCode 配置文件，添加如下配置

```javascript
  "editor.tabSize": 2,
  "files.associations": {
    "*.vue": "vue"
  },
  "eslint.autoFixOnSave": true,
  "eslint.options": {
    "extensions": [
      ".js",
      ".vue"
    ]
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue",
    "vue-html"
  ],
  "emmet.syntaxProfiles": {
    "javascript": "jsx",
    "vue": "html",
    "vue-html": "html"
  },
  // "prettier.singleQuote": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html"
```

PS：这里有一个不明白的地方，我在没有装 vscode 插件 Beautify 以及 Prettier 插件的时候，引用了上述配置也能生效。。。但建议大家将这两个插件都安装一下。

这样每次保存的时候就可以根据根目录下.eslintrc.js 你配置的 eslint 规则来检查和做一些简单的 fix。每个人和团队都有自己的代码规范，统一就好了

### 命令式自动修复

```bash
npm run lint -- --fix
```

命令行工具有几个选项，你可以通过运行 eslint -h 查看所有选项

<br>
