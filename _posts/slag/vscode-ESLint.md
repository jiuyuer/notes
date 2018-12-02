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
  // eslint
  "editor.tabSize": 2,
  //根据文件后缀名定义vue文件类型
  "files.associations": {
    "*.vue": "vue"
  },
  "eslint.autoFixOnSave": true, //每次保存的时候将代码按eslint格式进行修复
  "eslint.options": {
    "plugins": ["vue"],
    "extensions": [
      ".js",
      ".vue"
    ]
  },
  //保存时eslint自动修复错误
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue",
    "vue-html",
    {
      "language": "vue",
      "autoFix": true
    }
  ],
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force" // 可以换成上面任意一种value
    }
  }
```

PS：这里有一个不明白的地方，我在没有装 vscode 插件 Beautify 以及 Prettier 插件的时候，引用了上述配置也能生效。。。但建议大家将这两个插件都安装一下。

这样每次保存的时候就可以根据根目录下.eslintrc.js 你配置的 eslint 规则来检查和做一些简单的 fix。每个人和团队都有自己的代码规范，统一就好了

### ESLint 和 Prettier 的冲突修复

在用 `Prettier` 格式化的时候，可以能会和 `ESLint` 定义的校验规则冲突，比如 `Prettier` 字符串默认是用双引号而 `ESLint` 定义的是单引号的话这样格式化之后就不符合 `ESLint` 规则了。所以要解决冲突就需要在 `Prettier` 的规则配置里也配置上和 `ESLint` 一样的规则，这里贴下 `ESLint` 和 `Prettier` 的配置文件。

- .eslintrc.js 配置文件

```javascript
module.exports = {
  root: true,
  parser: "babel-eslint",
  parserOptions: {
    sourceType: "module"
  },
  env: {
    browser: true,
    node: true,
    es6: true
  },
  extends: "eslint:recommended",
  // required to lint *.vue files
  plugins: ["html"],
  // check if imports actually resolve
  settings: {
    "import/resolver": {
      webpack: {
        config: "build/webpack.base.conf.js"
      }
    }
  },
  // add your custom rules here
  //it is base on https://github.com/vuejs/eslint-config-vue
  rules: {
    "accessor-pairs": 2,
    "arrow-spacing": [
      2,
      {
        before: true,
        after: true
      }
    ]
  }
};
```

- .prettierrc 配置文件

```javascript
{
  "eslintIntegration": true,
  //使用单引号
  "singleQuote": true,
  //结尾不加分号
  "semi": false
}
```

这样把 `ESLint` 和 `Prettier` 冲突的规则配置一致,格式化之后就不会冲突了。

### 命令式自动修复

```bash
npm run lint -- --fix
```

命令行工具有几个选项，你可以通过运行 eslint -h 查看所有选项

<br>
