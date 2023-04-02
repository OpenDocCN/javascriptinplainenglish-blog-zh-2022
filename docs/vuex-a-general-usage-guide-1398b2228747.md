# Vuex:一般使用指南

> 原文：<https://javascript.plainenglish.io/vuex-a-general-usage-guide-1398b2228747?source=collection_archive---------10----------------------->

## 如何使用 Vuex

![](img/40a1f3b72aefa3da7811e333d8a7424b.png)

## 1.Vuex 简介

Vuex 是一个状态管理工具。所谓状态就是数据，有些数据就是通过这个工具来管理的。当多个组件需要相同的数据时，这些数据可以交给 Vuex 统一管理，组件可以直接引用这些数据，避免了组件之间繁琐的层层传递。

## 2.Vuex 内核

Vuex 有五个核心，状态、获取器、变异、动作和模块。状态用来存储要管理的数据，getter 相当于 computed 属性，变异用来定义方法修改状态中的数据，动作用来定义一些异步方法，模块可以把多个存储一分为一。模块。

## 3.Vuex 的使用

**3.1** 在一个 Vue 项目中使用 Vuex 时，需要先安装 Vuex 插件并注册。一般来说，会有的。使用下面的 index.vue 在 src 下创建一个新的存储文件夹，并在该文件中创建一个存储容器实例。

```
// *1\.* *Install the plugin*
npm install vuex --save
// *2\.* *Register plugin*
import Vue from 'vue' 
import Vuex from 'vuex'
Vue.use(Vuex)
```

**3.2** 创建一个 vuex 实例，在 vuex 上提供一个`Store()`方法创建实例，命名为 store，意思是仓库。在`Vuex.Store()`中传递一个配置对象。配置对象包括上述五个核心。如果不用，可以省略。

```
const store = new Vuex.Store({
    state: {num: 2}, // store data
    getters: {}, // computed property
    mutations: {}, // Some methods of modifying data in state
    actions: {}, // async method
    modules: {} // store module
})
export default store
```

**3.3** 引入条目文件 main.js 中的存储。

```
// main.js
import Vue from 'vue'
import App from './App'
import store from './store/index.vue' // **Shorthand** import store from './store'

Vue.config.productionTip = false

new Vue({
    el: '#app',
   store: store, // **es6 shorthand** directly write the store property name is the same as the variable name
   render: h => h(App)
})
```

**3.4** 如何使用页面上商店中的数据？在使用 vuex 中的数据之前，使用`import`导入写入的存储。在组件中，使用插值表达式中的`**$store.state.num**`获取存储中 num 的数据。

```
<template>
    <div>
        <h2>{{ $store.state.num }}</h2>
    </div>
</template>
```

4.mapState，mapMutations，mapGetters，mapActions 映射

```
1\. // First deconstruct four methods from vuex 
import {mapState, mapMutations, mapGetters, mapActions} from 'vuex'
2\. // Map state data and getters computed properties in computed computed properties
computed: {
    ...mapState('module name', ['name', 'age'])
    ...mapGetters('module name', ['getName'])
}
3\. // Mapping mutations and actions methods in methods method
methods: {
    ...mapMutations('module name', ['method name1','method name2'])
    ...mapActions('module name', ['method name1','method name2'])
}
4\. These data and methods can be called and obtained through this
```

以上是 vuex 的一般用法。谢谢你。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****