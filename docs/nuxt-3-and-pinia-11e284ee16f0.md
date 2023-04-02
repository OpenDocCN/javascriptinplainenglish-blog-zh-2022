# 带 Pinia 的 Nuxt 3 中的状态管理

> 原文：<https://javascript.plainenglish.io/nuxt-3-and-pinia-11e284ee16f0?source=collection_archive---------4----------------------->

## 集成 Pinia 作为 Nuxt 3 应用程序的状态管理库。

![](img/e12c8d5eae3b6ef3e500b9c3ca739604.png)

# Nuxt 3 和 Pinia

## Vuex ->皮尼亚

Vue 的创造者尤雨溪曾说过“皮尼亚实际上是 Vuex 5！在这一点上，这实际上是一个命名/品牌问题。”

就目前而言，最好还是关注 Pinia 的内容，而不是 Vuex。

![](img/f54625e9022111f5684f8c9a0aaba6a7.png)

我建议阅读 VueJS 的官方[帖子](https://vuejs.org/guide/scaling-up/state-management.html#pinia)来更好地理解为什么 Pinia > Vuex。

## 在 Nuxt 3 中安装 Pinia

Pinia 几乎为 Nuxt 3 提供了一流的支持。您需要安装两个软件包:

```
yarn add pinia
yarn add @pinia/nuxt
```

## 将 Pinia 添加到 nuxt.config 文件中

您需要将`'@pinia/nuxt'`添加到 buildModules 数组中。

```
// nuxt.config.js
import { defineNuxtConfig } from 'nuxt3'

export default defineNuxtConfig({
  buildModules: ['@pinia/nuxt'],
})
```

## 建立您的 Pinia 商店

现在构建一个命名商店。对于我的用例，我需要管理关于过滤器的状态，所以我的商店的框架如下所示:

```
// store/filters.js
import { defineStore } from 'pinia'

export const useFiltersStore = defineStore({
  id: 'filter-store',
  state: () => {
    return {
      filtersList: ['youtube', 'twitch'],
    }
  },
  actions: {},
  getters: {
    filtersList: state => state.filtersList,
  },
})
```

这只是展示了你的商店的总体结构。关键是`defineStore`，并确保包含一个`id`。在这种情况下，我使用`'filter-store'`作为我的 id，但它可以是您喜欢的任何东西。

通读 Pinia 的[文档](https://pinia.vuejs.org/core-concepts/)，更好地掌握如何正确使用 Pinia。

## 将 Pinia 引入 Vue 组件

有了我们的商店，只需将它导入到您想要使用的组件中，就可以玩得开心了！

```
<template>
  <div>
    {{ filtersList }}
  </div>
</template>

// components/FilterMenu.vue
<script>
import { useFiltersStore } from '~/store/filters'

export default defineComponent({
  setup() {
    const filtersStore = useFiltersStore()
    const filtersList = filtersStore.filtersList

    return { filtersList }
  },
})
</script>
```

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***