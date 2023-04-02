# 如何在 Nuxt 3 中使用 URL 查询参数

> 原文：<https://javascript.plainenglish.io/using-url-query-params-in-nuxt-3-eaa930419fa5?source=collection_archive---------6----------------------->

![](img/75d932bceca6eb389961a2f88e3e0b48.png)

> 这是我之前关于如何在 Nuxt 3 中设置查询参数的[帖子](https://codybontecou.com/silently-update-url-nuxt-3.html)的延续。我们将继续编写那里的代码，所以请务必检查它。

## 我们正在解决的问题

我们停止了我们的 URL 看起来像`localhost:3000/test?streamer=faker`。这很好，但包含了一些不太理想的情况。

因为 URL 参数是使用我们输入的 v-model 更新的，如果页面被刷新，我们将丢失本地状态和存储在`twitchStreamer`中的值。

## 在 Nuxt 中使用 useRoute

Nuxt.js 依赖于 [vue-router](https://router.vuejs.org/) 的大部分路由逻辑。

在我们的例子中，我们使用的是组合 API，这是 Nuxt 3 内置的新特性之一。

为了得到我们的路线，我们用把`useRoute()`带进我们的`setup()`。Nuxt 3 自动导入`useRoute()`，所以我们可以选择显式或隐式。

```
setup() {
  const route = useRoute()
}
```

拥有我们的路线可以解锁`vue-router`的所有好处，包括访问我们的查询参数！

## 使查询参数持久化

通过访问我们的路线，我们可以使用`route.query.streamer`检查查询变量(在`streamer=`中的=之后是什么)。

轻松点。

我现在将这个逻辑与一个带有`twitchStreamer`变量的[三元运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)一起使用。

```
const twitchStreamer = ref(route.query.streamer ? route.query.streamer : '')
```

现在，每次页面被导航或刷新时，我们的`twitchStreamer`将检查我们的`route`是否有一个 streamer 查询参数。

如果是，我们的`twitchStreamer`将包含参数的值。否则，它将是一个空字符串。

## 最终代码片段

```
<!-- pages/example.vue -->
<template>
  <input v-model="twitchStreamer" />
</template>

<script>
  setup() {
    const route = useRoute()
    const router = useRouter()
    const twitchStreamer = ref(route.query.streamer ? route.query.streamer : '')

    watch(twitchStreamer, (twitchStreamer, previous) => {
      router.push({
        path: '/test',
        query: { streamer: twitchStreamer },
      })
    })

    return { twitchStreamer }
</script>
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*