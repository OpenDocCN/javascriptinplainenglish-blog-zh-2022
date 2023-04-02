# 回到 Vue 2 快速掌握 Vue 3

> 原文：<https://javascript.plainenglish.io/back-to-vue-2-to-quickly-master-vue-3-a2644da8efbc?source=collection_archive---------7----------------------->

## 通过与 Vue 2 的比较，很好地掌握 Vue 3 的特性。

![](img/b4121ad5ce67f1ab21f0fab46713fc0a.png)

Photo by [Rovshan Allahverdiyev](https://unsplash.com/@hi_i_am_rovshan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/classic?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

很久没有和 Vue.js 合作过真正的工作项目了。最近，我在空闲时间为 Vue 3 做了更多的研究。我从 Vue 3 上发现了很多有趣的东西。我认为，当我们开始使用任何框架的新版本时，我们都会有一个问题。这个问题是“如何做…就像我使用这个框架的旧版本时一样？”我还意识到，我们有一个更快学习新知识的好方法，那就是把我们带回到旧版本，并应用新知识。这也是为什么我会用 Vue 2 和 Vue 3 列举和对比一些案例。我觉得会帮助我们快速学习 Vue 3。

# 选项 API 和组合 API

Composition API 是 Vue 3 为我们提供的最好的特性之一。复合 API 有许多有趣的特性。这也是我们选择 Vue 3 组合 API 和 Vue 2 选项 API 来开始这篇文章的原因。首先，我将展示一个带有组合 API 和选项 API 的 Vue.js 组件的基本示例:

使用可选 API 的 Vue 2 基本组件:

Vue 3 中带有组合 API 的基本组件:

如果你想在 Vue 3 中写得更短，可以用`setup script`试试:

上面，我展示了用一个设置脚本在 Vue 2、Vue 3 和 Vue 3 中创建一个包含数据、方法、已安装和已卸载事件的基本 Vue.js 组件的三种方法。我想你可以看到它们之间的一些不同之处，我现在就来谈谈它们。

**状态**

状态或另一个名称—数据是 Vue 中的重要功能之一，它支持我们使用自己的反应数据进行工作。让我们看看如何在 Vue 2 和 Vue 3 中处理状态。

在 Vue 2 中，状态在`data`中被定义为一个函数返回，一个对象包含我们的状态。这里有一个例子:

```
data(){
  return {
    name: 'Tasy'
  }
}
```

在 Vue 3 中，状态将由`ref`和`reactive`在`setup`中定义。这里有一个例子:

```
const name = ref('Tasy');
const user = reactive({name: 'Tasy'});
```

与 Vue 2 或选项 API 不同，使用组合 API，我们有两个函数来生成反应数据，分别是`ref`和`reactive`。

**生命周期**

在 Vue 2 中，我们有许多生命周期挂钩，它们在主对象中被定义为属性。使用 Vue 3，我们可以在`setup`内部将它们定义为函数调用。在上面，我展示了一个例子，如何用 onMounted 和 onUnmounted 定义一个 Vue 3 生命周期钩子。对于其余的挂钩，我将在这里向您展示选项 API 和组合 API 中的生命周期挂钩表:

如您所见，选项 API 中的生命周期挂钩几乎与组合 API 中的生命周期挂钩相同。除了名字和使用它们的方式，我们还有一些其他不同的东西。在 Vue 2 中，我们有两个生命周期挂钩，分别是`created`和`beforeCreate`。它们在 Vue 3 中被移除了，我们可以把我们的逻辑移到`setup`中。另一件不同的事情是，在 Vue 2 中，我们只把所有代码放在每个钩子的一个地方。在 Vue 3 中，我们可以在`setup`的很多地方这样定义它:

```
setup(){
  onMounted(() => {
    // mounted 1
  })
  onMounted(() => {
    // mounted 2
  })
}
```

**计算出的**

`computed`是格式化或处理输出数据并在 Vue.js 组件中修改它的好方法之一。在 Vue 2 中，我们可以使用`computed`作为组件属性计算的函数，如下所示:

在 Vue 3 中，Composition API 为我们提供了一个函数`computed`来定义我们在`setup`内部的计算。我们可以看到下面的例子:

**手表**

Vue.js 的另一个重要特性是`watch`，它帮助我们在数据改变时调用我的回调。在 Vue 2 中，`watch`被定义为与`computed`几乎相同，是 Vue.js 组件中的一个对象。属性名是状态或属性的名称，值可以是函数，数组或字符串。这是经典腕表的一个简单组件:

除了上面的方法，在 Vue 2 中我们还有很多其他的方法来处理`watch`。在 Vue 3 中，`watch`与`computed`也几乎相同。用 source、callback、option(可选)等三个参数在`setup`内部调用即可。如果要为数据定义多个处理程序，只需多次调用`watch`即可。下面是 Vue 3 中手表的一个简单例子:

用起来这么简单，我真的很喜欢这个。除此之外，Vue 3 提供了一个有用的特性，即`watchEffect`，它可以帮助我们在依赖关系改变时运行回调。你可以在这里看到一个例子:

**组件**

说到组件，Vue 2 和 Vue 3 没有太多区别。只需将我们想要使用的组件推入对象组件:

在 Vue 3 中，我们有了一种新的方法来用`setup script`导入更短的组件:

**方法**

Vue 2 中的方法与`computed`和`watch`相同，它们在属性方法中被定义为包含我们函数的对象。它看起来会像这样:

```
export default {
  methods: {
    sayHi() {
      console.log('Hi guys');
    }
  }
}
```

在 Vue 3 中，我们只需要在`setup`内部创建一个函数来制作一个方法。太简单了:

```
export default {
  setup() {
    function sayHi() {
      console.log('Hi guys');
    }
  }
}
```

选项 API 和组合 API 之间有一些基本的区别。

# 组件通信

我认为每个应用程序也有许多组件，它们需要一起通信来运行我们的应用程序。非常重要！所以 Vue.js 在两个 Vue.js 版本中为我们提供了很多方法。现在，让我们回到 Vue 2 中的通信，并学习如何在 Vue 3 中做同样的事情。

**道具和发射**

Vue.js 中父组件与子组件之间最基本的通信方式。父组件使用`props`将值传递给子组件，子组件通过`emit`触发父组件中的某个事件。在 Vue 2 中，我们可以为属性 **props** 中的组件定义一个 props 列表，并使用来自 **this** 的数据。关于`emit`，Vue 2 给我们提供了方法**这个。$emit('eventName '，value)** 用值向父组件发出事件(可选)。下面是一个有道具**号** 并能发出事件“更新”的组件的例子:

在 Vue 3 中，我们有很多方法可以使用`props`。如果想保留属性道具为 Vue 2，可以用`setup`函数的第一个参数得到。然后通过函数`toRefs`或`reRef`访问其值。关于`emit`，我们可以从`setup`(上下文)的第二个参数调用它来做那个工作，而不是**这个。$emit()** 。这里有一个例子:

除此之外，Vue 3 为我们提供了有用的方法`defineProps`，它支持我们使用`props`设置脚本的工作。用 Vue 2 中与`props`相同的对象调用`defineProps`，返回一个 prop 实例。然后我们可以使用`toRefs`和`toRef`来访问来自`defineProps`的结果。关于`emit`，Vue 3 给了我们一个新的功能`defineEmits`来配合 emit。这个函数将返回一个实例来帮助我们触发之前定义的事件。下面是这种方式的一个例子:

在我看来，我真的很喜欢用`setup script`的第二种方式。请注意`definneProps`和`defineEmit`只在设置脚本中使用，不需要从 Vue.js 导入。

**提供并注入**

正如我在上面所说的，在我们有许多组件的真实项目中，我们将有一个大的组件树。这就产生了[钻柱](https://vuejs.org/guide/components/provide-inject.html#prop-drilling)的问题。为了帮助我们处理这个问题，Vue.js 提供了一个名为 Provide and Inject 的功能。它允许我们向组件的后代提供数据。这是一个例子:

在根组件中，只需要将 provide property(对于数据几乎是一样的)定义为一个返回对象的函数。在组件的后代中，我们只需要用一个数组的值来定义 inject 属性，该数组的名称是我们想从根组件中使用的。如果你想让`provide`和`inject`变成反应数据，我想我们可以应用`computed`来做这项工作:

在 Vue 3 中，我们可以使用设置功能中的功能`provide`和`inject`。它简单易用:

**插槽**

这是一种将父视图放在另一个组件视图中的方法。对于插槽，两个版本基本相同。以下是两个版本的示例:

我们只是在他们之间有一点点变化，这是属性`$slots`。在 Vue 2 中，该属性返回的对象的键是槽名，值是 VNode 数组。在 Vue 3 中，这个属性返回相同的对象，键作为槽的名称，但是值是一个返回 VNode 数组的函数。

另外， **$scopedSlots** 将在 Vue 3 中被移除。

# **代码可重用性**

在 Vue 中，我们有很多方法来重用我们的代码(全局属性、插件、扩展、混合等等)。).Vue 3 也涵盖了那些方法，并对它们做了一些优化。

**全局属性**

在 Vue 2 中，如果我们想创建一些全局属性，我们可以像这样访问 Vue.js 的属性`prototype`:

```
Vue.prototype.$axios = axios({});
```

上面这种方式在 Vue 3 中是不允许的。如果我们想创建一个全局属性，Vue 3 为我们提供了另一种从 Vue.js 应用实例的属性`config`到属性`globalProperties`的方法。让我们看一个简单的例子:

```
const app = createApp({});
app.config.globalProperties.$axios = axios({})
```

**混音和定制挂钩**

`Mixins`是一种灵活的方式，当我们想要为许多组件重用我们的代码、逻辑时，它可以为我们提供支持。它为我们提供了一个工具，可以在我们想要的每个组件中应用我们的数据、方法或一些逻辑。这里有一个`mixins`的例子:

在这个例子中，我们用一个数字的数据和一个增加这个数字的值的方法创建了 mixins。如果我们想要实现这个逻辑，我们只需要将这些 mixin 添加到组件的 mixin 数组中。之后，您的组件将拥有该数据和方法。我知道这是一种在 Vue.js 中重用代码的有用方法，我在许多项目中都应用了这种方法。但是如果 mixins 被滥用或大量使用，我们可能会在数据、方法等方面遇到一些问题。

在 Vue 3 中，我们有另一种更清晰的方式来完成这项工作。这是定制挂钩。在定制钩子中，我们可以打包我们的逻辑，只导出我们想要的。下面是一个自定义钩子的例子，它的工作与上面的例子相同:

我真的很喜欢这种方式，我认为它将是我们在 Vue 3 项目中的好朋友。顺便说一下，我这里有一篇关于“如何编写 10 个有用的 Vue.js 自定义钩子”的文章:

[](/10-useful-custom-hooks-with-vue-js-37f0fd42ce0d) [## Vue.js 的 10 个有用的自定义挂钩

### Vue.js 是我使用的第一个 JavaScript 框架。我可以说 Vue.js 是我打开进入的第一扇门之一…

javascript.plainenglish.io](/10-useful-custom-hooks-with-vue-js-37f0fd42ce0d) 

# 模型

`Model`是一个很棒的 Vue.js 特性，它帮助我们处理双向数据绑定。在这一部分，我会讲 HTML 输入元素的`model`和自定义组件的`model`。我们走吧。

**HTML 输入元素**

对于 input 组件，如果要将一个状态与 input 元素绑定，只需要使用`v-model` with value 作为这个状态的名称即可。两个版本是一样的。

Vue 2:

Vue 3:

**自定义组件**

对于自定义组件，我们在 Vue 3 中有许多更新，使这个功能更加灵活。在谈论这个之前，我们将回到 Vue 2 来了解如何为一个自定义组件制作一个`model`。为此，我们需要将`props`和`model`混合一点。以下是我的例子:

我将解释一下这个例子。在自定义输入组件中，我将带有值的属性`model`定义为具有两个属性`prop`和`event`的对象。`prop`是您想要 v-model 绑定的属性名(该属性的缺省值是“value”)。`event`是您需要向数据已经更改的父组件发出的事件名称(该属性的默认值是“input”)。为您的模型定义属性名称是很重要的(如果您想要使用默认的模型值，请使用“value”)。

在 Vue 3 中，除了绑定一个模型，我们还可以为每个定制组件绑定多个模型。基本上，到的方式与 Vue 2 几乎相同，只是有一些变化。首先，`v-model`的默认属性名从“值”变为“模型值”。其次，将使用规则`update:<model name>`设置发射事件名称(例如:`update:title`)。为了绑定到组件的子模型，我们将使用此规则`v-model:<name>`进行键入。下面是一个关于有文本框和复选框的组件的例子，`v-model`表示文本框数据，`v-model:checked`表示复选框的选中状态:

我认为没有必要对这个例子做更多的解释，因为它和 Vue 2 的例子几乎是同一个概念。只要改变一点语法，按照我上面说的规则名称。然后，我们有一个自定义组件，它可以与多个模型一起工作。对于那些喜欢使用`setup script`的人来说，这里有一个我们构建上述组件的例子:

以上是在 Vue 3 中使用`model`的两个例子。

# 结论

在这篇文章中，我通过回顾 Vue 2 分享了一些关于 Vue 3 的新特性。我个人非常喜欢这种学习新功能的方式。我有一些理由:

*   带自己回到旧版本可以确保我们不会错过旧版本的任何东西。我呢，是在写这篇文章的时候在 Vue.js 里面了解到`v-model`的。我以前没用过这个功能。
*   了解新版本有哪些改进的最好方法之一是回到旧版本。
*   对比新旧版本中的代码可以帮助我们更快地理解它。个人认为新版本的语法往往比老版本短。所以新版本中的一些代码行可能是旧版本中的许多行(步骤)。阅读旧版本的代码可以让我们知道新版本的代码是做什么的。

这些就是我今天想要分享的东西。希望这篇文章对你有帮助。阅读 Vue 3 和 Vue 2 文档中的更多信息:

[](https://vuejs.org/guide/introduction.html) [## 简介| Vue.js

### 您正在阅读 Vue 3 的文档！Vue 是一个 JavaScript 框架，用于构建…

vuejs.org](https://vuejs.org/guide/introduction.html) [](https://v2.vuejs.org/v2/guide/) [## 简介- Vue.js

### vue . js——渐进式 JavaScript 框架

v2.vuejs.org](https://v2.vuejs.org/v2/guide/) ![](img/9bb0437e8fe71ea96db04bf6f110b01c.png)

Photo by [Thái An](https://unsplash.com/@johnn21?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/saigon?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

感谢您的阅读。

通过 [Linkedin](https://www.linkedin.com/in/thaisangnguyen3894/) 或 [Twitter](https://twitter.com/tasyit) 与我联系。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*