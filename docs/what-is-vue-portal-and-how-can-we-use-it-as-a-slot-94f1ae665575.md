# 什么是端口值，我们如何将其用作插槽

> 原文：<https://javascript.plainenglish.io/what-is-vue-portal-and-how-can-we-use-it-as-a-slot-94f1ae665575?source=collection_archive---------13----------------------->

## PortalVue 可能是一个非常有用的特性，可以使您的项目更加动态。

你知道我们不能用一个孩子的孩子的插槽吗？现在你知道了。但是，如果我们有这种结构，我们绝对必须这样做呢？嗯，有一个解决办法。

![](img/4f314ad4b9d0cb3d9427969803a0c75f.png)

在做一个项目的时候，我遇到了一个问题，当我不得不从孩子的孩子的父母组件中显示一个槽时。据我所知，仅仅依靠简单的插槽是不可能实现的。

幸运的是， ***有一个不同的解决方案*** 可以解决我的问题。

***如果你正在使用 Vue2，并且有和我一样的问题，欢迎你阅读这篇文章。***

# 安装门阀

首先，让我们在项目中安装 PortalVue，看看如何使用它来代替下面例子中的插槽:

```
npm install --save portal-vue
```

并且能够在项目中使用它。

```
import PortalVue from 'portal-vue'

Vue.use(PortalVue)
```

所有这些信息你都可以在官方文档页面上找到，[在这里](https://portal-vue.linusb.org/guide/getting-started.html#setup)。

然而，即使你已经可以在官方页面上找到它，我还是想谈谈安装的原因是，即使有了那些配置，PortalVue 的元素在我的项目上也不能被识别。

为了解决这个问题，你可以直接把它导入到组件中，或者 ***把它作为一个组件导入，但是在全局级别*** (更好的解决方案)。

在你的 ***main.js*** 中，就这样导入:

```
import { Portal, PortalTarget } from 'portal-vue'Vue.component('portal', Portal) 
Vue.component('portal-target', PortalTarget)
```

# 把它当作一个插槽

你可以在他们的官方页面上找到许多不同的 PortalVue 用法的例子，但在这篇文章中，我想注意一下 ***使用它而不是槽*** 的问题。

***父- >子(1)——>子(2)***

这意味着我希望在组件“Child (2)”中有一个槽，并将它传递给组件“Parent”。

让我们开始吧。

```
// Child (2)<template>
   <div>
     <portal-target name="content"/>
   </div>
</template>
```

在上面的例子中，我们有一个“Child (2)”组件，我们希望在其中显示一些内容，我们将把这些内容传递给“Parent”组件。

为此，我们需要使用***" portal-target "***元素，并为其设置一个特定的名称。

嗯，在子组件(1)中，我们将只拥有导入的子组件(2)。

```
<template>
  <div>
    <Child2/>
  </div>
<template>
```

如你所见，我们没有传递任何道具给它。

而在我们的父组件中，我们还有另一个新元素，***【portal】***，其中我们要传递***【portal-target】的名称。***

```
<template>
   <div>
   <portal to="content">
       <div>
          <p>Some content to display in Child (2)</p>
       </div>
   </portal>
</template>
```

差不多就是这样了。

# 结论

PortalVue 可能是一个非常有用的特性，可以使您的项目更加动态。最棒的是，你可以将数据内容从**任何**组件传递到**任何地方**的**任何**其他组件，即使它不是嵌套的子组件。

## 我希望这对你有用！编码快乐！🚀

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*