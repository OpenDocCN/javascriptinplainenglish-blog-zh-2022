# 使用角形异步管道，让您的生活更轻松

> 原文：<https://javascript.plainenglish.io/angular-async-pipe-714dd864adaa?source=collection_archive---------6----------------------->

## 角异步管道

## 尽可能使用异步管道。让 Angular 为您做繁重的工作吧！

![](img/795ee5a2b0db800e631c7cfa70388298.png)

Photo by [Victor Freitas](https://unsplash.com/@victorfreitas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

AsyncPipe 是 Angular 提供的工具之一，让我们的生活变得更加轻松。根据官方文档， ***异步管道*** 做 4 件事:

1.  它自动订阅一个`Observable`(或`Promise`)并返回最新发出的值。
2.  每当发出一个新值时，它就标记关联的组件以进行更改检测。
3.  如果表达式的引用发生变化，它会自动退订旧的`Observable`，并订阅新的。
4.  当组件被销毁时，它会自动取消订阅以避免内存泄漏。

让我们使用一个演示应用程序来详细检查每一点。

在我们的演示应用程序中，我们有 2 个组件:使用**异步管道**、*、*的`DopeComponent`和不使用的`RegularComponent`。

我们将比较这些实现，并强调在不使用异步管道时我们必须做的额外工作。

两个组件[都通过一个`@Input()`修饰属性从它们的父组件](/angular-component-communication-81e5e02c6cbe)接收数据，这个属性是一个`Observable`。

如果你不熟悉可观测量，可以把它们想象成异步数据流。它们用于异步发出值。但是为了接收发出的值，必须首先订阅它们。

`DopeComponent`的类中只有修饰属性。

在各自的模板文件中使用的*异步管道*负责我们提到的所有事情。

另一方面，`RegularComponent`就没那么简单了。让我们看看在这种特定情况下各自的实现是什么样的，并逐一说明。

首先，我们需要手动订阅。我们在`ngOnChanges`方法中这样做，并将值赋给一个局部变量(第 21 行和第 29–31 行)。所以，第一次可观察的被传递，我们订阅它。

接下来，我们需要跟踪订阅。我们首先声明变量(第 9 行),然后分配订阅(第 21 行),以便在组件销毁时取消订阅(第 25–27 行)。我们需要这样做来避免内存泄漏。

由于两个组件都使用`OnPush`变更检测策略，变更检测只有在非常特殊的情况下才会被触发。要了解更多关于`OnPush`变化检测策略的工作原理，您可以观看此视频:

YouTube video by [Angular University](https://www.youtube.com/channel/UC3cEGKhg3OERn-ihVsJcb7A)

回到我们的演示，异步管道会处理这个问题，我们不必担心变化检测。

然而，在`RegularComponent`中，我们必须注入`ChangeDetectorRef`(第 12 行)并手动标记用于变更检测的组件(第 32 行)。

***注:*** *还有其他方法来实现这一点，以达到相同的结果。请记住，这只是为了演示。*

最后，如果表达式的引用发生变化，`RegularComponent`不会自动订阅新的可观察值。这意味着我们必须再多走一步，实现这一点。

我们在`ngOnChanges`生命周期挂钩方法中这样做。我们取消订阅之前的`Observable`(第 15-18 行)，然后订阅新的(第 20-22 行)。

咻，这么多工作！这款 ***AsyncPipe*** 肯定是游戏规则的改变者，对吧？

和往常一样，你可以在下面的 StackBlitz 找到一个工作演示，或者只在[这个 GitHub 库](https://github.com/kagklis/ng-async-pipe-demo)中找到代码。

最后，不要忘记[订阅我的时事通讯](https://vkagklis.medium.com/subscribe)来关注更多类似的内容！

# 结论

在本文中，我们研究了**异步管道**以及它能为我们做的所有工作。不要努力工作，要聪明工作。只要有可能，就用这根管子。让 Angular 为您做这项工作。

感谢阅读！我希望你喜欢这篇文章，并且你学到了一些新的东西。

编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*与* [***不和***](https://discord.gg/GtDtUAvyhW) *。*

***供进一步阅读:***

[](/angular-interceptors-a-complete-guide-7294e2317ecf) [## 角度截击机——完全指南

### 关于 Angular 中的截击机，你需要知道的一切。

javascript.plainenglish.io](/angular-interceptors-a-complete-guide-7294e2317ecf) [](https://betterprogramming.pub/split-angular-nested-forms-into-subform-components-dcf32d1fb10d) [## 将角形嵌套形状拆分为子形状构件

### 如何将有角度的嵌套形状变成更小的子形状组件

better 编程. pub](https://betterprogramming.pub/split-angular-nested-forms-into-subform-components-dcf32d1fb10d) [](/angular-route-parameters-a-simple-guide-88c69d54102c) [## 角度布线参数:简单指南

### Angular 的布线参数以及如何在布线元件之间传递小块信息的概述。

javascript.plainenglish.io](/angular-route-parameters-a-simple-guide-88c69d54102c)