# 你不应该再在 Vue.js 中使用 Mixins 了

> 原文：<https://javascript.plainenglish.io/you-shouldnt-be-using-mixins-in-vue-js-anymore-ec8c09824f9f?source=collection_archive---------1----------------------->

![](img/1d6ae1e934451544b1e218d086346936.png)

Photo by [Greyson Joralemon](https://unsplash.com/@greysonjoralemon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Mixins 是 Vue 2 中组件间共享可重用逻辑的首选方式。但是现在有了组合 API，我们可以用更干净的方式实现代码重用。

# 什么是混合蛋白？

mixin 是通过将 mixin 的属性与组件合并来在组件之间重用功能的一种方式。它允许我们一次定义某个逻辑，并在多个组件上使用它。

# 为什么我不应该使用 mixins？

嗯，混合通常不是共享逻辑的理想方式，因为它们有一些缺点:

## 重名

命名冲突经常出现在混合中。在合并过程中，mixins 和组件之间冲突的属性会基于某种合并策略被覆盖。这可能会在我们的应用程序中导致一些意外的行为。

## 紧密结合

mixin 和组件之间的隐式依赖并不少见。这使得在不破坏现有代码的情况下重构组件或 mixin 变得异常困难。随着时间的推移，随着新需求的出现，mixin 也可以与其他 mixin 紧密耦合。

## 难以理解和调试

对于一个新的开发者来说，理解一个有很多混合代码的代码库是非常困难的。属性来自哪里并不明显，尤其是如果有全局注册的 mixins。随着应用程序的增长，隔离 bug 也变成了一场噩梦。

# 用组件替换混合组件

让我们从一个例子开始，来说明 mixins 的一些缺陷，以及我们如何用组合 API 解决这些问题。

假设我们有一个简单的倒计时器，在显示组件的主要内容之前等待几秒钟。我们将这个逻辑提取到一个名为`countDownMixin`的 mixin 中。代码如下所示:

通过注册这个 mixin，我们将能够把递减计数逻辑“混合”到组件中。

乍一看，这似乎是一个很好的解决方案，但是如果我想等待 20 秒而不是 10 秒呢？

一个解决方案是从消费组件覆盖`countDown`的初始状态。通过这样做，我们显式地创建了冲突的名称，因为我们知道组件中定义的数据属性将被赋予最高优先级。

这种解决方案是可行的，但是拥有这种能力也使得 mixin 容易受到其他选项的无意替换。现在，如果组件定义了一个`decrement`方法，而不知道`countDownMixin`也有一个同名的方法，那么组件将不再像预期的那样工作。

尽管`decrement`方法被定义为仅供内部使用，但它不可能不被覆盖。

## 使用组合 API 的更好的解决方案

通过使用 Composition API，我们避免了使用 mixins 时面临的所有问题。`useCountDown` composable 将倒计时持续时间作为一个参数。不需要覆盖任何东西，依赖关系被整齐地组织为可组合函数的参数。

它还公开了仅供消费组件使用的属性，并且内部状态受到保护，因此组件不会意外改变可组合组件的行为。

名称重叠也不是问题，因为我们需要显式地为所有返回的可组合变量提供名称。

# 结束语

组合 API 使得代码重用变得非常简单明了。我希望这篇文章足以说服您从 mixins 中迁移出来，接受 composables 的力量。如果你需要更多关于组合 API 的信息，请查看[官方文档](https://v3.vuejs.org/guide/composition-api-introduction.html)。感谢您的阅读。

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*