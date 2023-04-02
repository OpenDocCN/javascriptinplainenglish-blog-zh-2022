# 看看 Redux connect()函数

> 原文：<https://javascript.plainenglish.io/a-look-at-the-redux-connect-function-8b7c1fb8e357?source=collection_archive---------9----------------------->

众所周知，React 是当今构建用户界面(ui)最流行的库之一。我相信阅读这篇博客的大多数人在之前的项目中都使用过 Redux 来管理应用程序的整体状态。

想知道 redux connect()函数是如何工作的吗？或者说编写 connect()函数涉及的各种 JavaScript 概念是什么？

在这种情况下，我将向您介绍编写我们自己的 connect()函数所涉及的 JavaScript 概念，然后可以将该函数集成到 Redux 库中并结合使用。

![](img/96e48e2be88309dc0aca5d328aed444a.png)

## ***根据 Redux 文档，connect()函数返回***

> connect()的返回是一个包装器函数，它接受您的组件并返回一个包装器组件及其注入的附加属性。大多数情况下，包装器函数会被立即调用，而不会保存在临时变量:`export default connect(mapStateToProps, mapDispatchToProps)(Component)`中。

首先，让我们看看 JavaScript 中的高阶函数。

> **什么是高阶函数？**

JavaScript 将函数视为一等公民，这意味着一个函数可以返回另一个函数，或者一个函数可以作为参数传递给其他函数，甚至可以将函数作为值存储在变量中。

基本上，高阶函数只是返回另一个函数或接受一个函数作为参数的函数。

***Redux 的 connect()函数是一个高阶函数，它以两个函数作为参数(mapStateToProps 和 mapDispatchToProps)，它还返回一个包装组件的函数。***

现在我们已经看到了 Redux 的 connect()函数的上述实现，我们知道 connect()是一个高阶函数。在编写我们自己的 connect()函数之前，我们需要了解闭包和 curry。

## **阿谀奉承**

Currying 是函数式编程中的一个过程，在这个过程中，我们可以将一个具有多个参数的函数转换成一系列嵌套函数。它返回一个新函数，该函数需要内联的下一个参数。

这里有一个 JavaScript 的例子:

迷茫？这个概念如何应用于现实世界的场景。让我给你一个场景。

*在我们的应用中，有些计算结果需要加倍。我们通常通过以下方式将带有 2 的结果作为参数传递给 multiply 函数:multiply(result，2)；*

*一个函数可以从 currying 返回，因此如果需要，它可以被存储并与其他参数集一起使用。*

希望您已经了解了 redux 如何使用 currying 实现 connect()()函数。

```
export default connect(mapStateToProps, mapDispatchToProps)(OurComponent);
```

## **关闭**

闭包只是指内部函数可以访问外部函数的范围，即使在外部函数已经被执行并从调用栈中移除之后。

假设我们有一个外函数 A 和一个内函数 b。

从高阶函数 Currying 的概念中，我们了解到 connect()()函数是一个 HOF(高阶函数),它接受两个函数作为参数，并返回一个匿名函数，我们通过使用 Currying 调用它来包装我们的组件。

*因此 connect()是一个外部函数，而返回的匿名函数是一个内部函数，所以传递给 connect()的属性可以被匿名内部函数访问，即使在 connect()使用闭包完成执行之后。*

*现在所有这些都准备好了，让我们继续编写我们自己的 connect()函数*

***我们自己写 connect()函数***

*我们将使用一个 starter 应用程序计数器，它具有连接到 redux 存储的递增/递减操作。所以计划是先编写我们自己的 connect 函数，然后将工作应用程序与它集成。*

计数器应用程序的 GitHub 链接如下:

[Github-own _ connect _ fn _ starter](https://github.com/itzzmeakhi/blog-code-rep/tree/main/own-connect-fn-starter)

![](img/5d9e0c2215d48bbf06c003fd40cd4904.png)

*一个简单的计数器应用程序，其中的计数器值存储在 redux store 中，可以通过调度 redux 操作和更新 reducer 来递增或递减。计数器组件使用 react-redux connect()函数连接到 redux 存储。*

我们的理解是 connect()是一个 HOF(高阶函数)，以两个函数为自变量，返回一个匿名函数。让我们以这个想法为基础。

现在，匿名函数接收我们的组件作为参数，我们可以通过 Currying 传递它。接下来，我们将在匿名函数中创建匿名类组件，该类将由匿名函数返回。

这里，我们使用一个匿名类来返回基于 HOF 模式的匿名函数中的 WrappedComponent。

我们现在可以传递组件属性以及 mapStateToProps 和 mapDispatchToProps 生成的属性。该实现声明 mapStateToProps 需要一个总体 redux 状态和组件属性作为参数，而 mapDispatchToProps 需要一个调度函数和组件属性作为参数。

可以用 this.props 访问组件 props，但是我们如何获得 redux store 的状态和分派方法呢？

在将 redux 集成到我们的应用程序的过程中，将会创建一个商店。我们将导出该存储并将其导入到我们的 connectFn 文件中。我们可以使用存储对象来访问它们。

还有工作要做。此时，您可能会观察到屏幕上显示的组件没有任何错误，但是当单击递增/递减时，计数器的值不会更新。这是因为每当组件的状态改变时，我们都必须重新渲染它。

我们可以通过订阅存储并在状态发生变化时呈现它来做到这一点。

我们可以导入连接 Fn，并且可以如下使用:

```
export default connectFn(mapStateToProps, mapDispatchToProps)(Counter);
```

就是这样！我们构建了自己的 connect()函数，并将其与 Redux 存储集成在一起。

[Github repo](https://github.com/itzzmeakhi/blog-code-rep/tree/main/own-connect-fn-final) 中的最终代码

希望这是有用的
❤️将是真棒😊

# 快乐编码

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*