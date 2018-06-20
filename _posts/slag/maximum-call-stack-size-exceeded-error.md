---
title: Vue.js “Maximum call stack size exceeded” error.
tags:
  - JavaScript
  - Vue.js
  - Error
categories:
  - 技术渣
date: 2018-06-20 10:04:46
---

在使用 Vuejs 开发 SPA 页面时，我创建了一个父组件以及子组件，然后通过父组件去调用子组件时，报如下错误：

```bush
Vue.js “Maximum call stack size exceeded” error.
```

示例代码：

> **Panel.vue**

```javascript
<template>
  <div id="panel">
    <div class="panel">
      <ul>
        <li v-for="shelf in shelfs">
          <panel-body :shelf="shelf" :selected.sync="selected"></panel-body>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import PanelBody from '../components/PanelBody'
export default {
  name: 'panel-body',
  components: {
    'panel-body': PanelBody
  },
  data: () => ({
    shelfs: [{
      name: 'shelf 1',
      books: [{
        title: 'Lorem ipum'
      }, {
        title: 'Dolor sit amet'
      }]
    }, {
      name: 'shelf 2',
      books: [{
        title: 'Ipsum lorem'
      }, {
        title: 'Amet sit dolor'
      }]
    }],
    selected: {}
  })
}
</script>
```

> **PanelBody.vue**

```javascript
<template>
  <div id="panel-body">
    <a href="#" v-on:click.prevent.stop="select">{{ shelf.name }}</a>
    <ul v-show="isSelected">
      <li v-for="book in shelf.books">{{ book.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'panel-body',
  props: ['shelf', 'selected'],
  computed: {
    isSelected: function () {
      return this.selected === this.shelf
    }
  },
  methods: {
    select: function () {
      this.selected = this.shelf
    }
  }
}
</script>
```

错误原因：

> Maximum call stack size exceeded

错误出处：

```javascript
import PanelBody from '../components/PanelBody'
export default {
  name: 'panel-body',
  components: {
    'panel-body': PanelBody
  },
```

错误解决：
你定义你的父组件名称:“panel-body”。**只要将名称改成:“panel”或者其他不与子组件引用名一样**，你就能删除你的循环引用，从而不再报错。
<br>