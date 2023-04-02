# 反应错误处理

> 原文：<https://javascript.plainenglish.io/react-error-handling-e64f9724dc15?source=collection_archive---------21----------------------->

![](img/a476f42523a567e5d0d1f9247e99dd08.png)

当我们用任何技术创建应用程序时，正确处理错误是必不可少的。组件树中任何地方出现的错误都会导致整个应用程序瘫痪。当一个项目有一个大的组件树时，开发人员在调试代码和确定错误发生的位置时会遇到困难。

React 16 引入了错误边界的概念来解决这些问题。错误边界是 React 组件，它捕捉子组件树中任何位置的 Javascript 错误，并通过回退 UI 显示可感知的错误消息。

这些错误边界只捕捉渲染、生命周期方法和内部钩子(如 useEffect)以及它们下面整棵树的构造函数中的错误。根据 React 文档，错误边界不会捕捉以下错误:

*   事件处理程序
*   异步代码(例如 setTimeout 或 requestAnimationFrame 回调)
*   服务器端渲染
*   在错误边界本身(而不是其子代)中抛出的错误
    为了创建一个错误边界，我们必须创建一个类组件
    ，它将拥有生命周期方法中的一个或两个。

为了创建一个错误边界，我们必须创建一个类组件
,除了 render()方法之外，它还将具有一个或两个生命周期方法。

1.  **getderivedstatefromrerror()**—这是一个静态方法，在渲染过程中，当子进程中的任何地方发生错误时，都会调用该方法来更新错误边界的状态，并用于触发回退 UI。
2.  **componentDidCatch()** —这用于在我们的错误边界组件捕获到错误时执行日志记录之类的操作。

> 根据 React 文档，React 团队还没有为功能组件提供错误边界支持，然而也没有与**getderivedstatefromrerror**和 **componentDidCatch** 生命周期等价的挂钩。

# **在哪里放置误差边界**

我们可以把误差边界放在任何需要的地方。我们可以在应用程序的顶层使用错误边界，即在应用程序组件的顶部，或者将它包装在单个组件上以单独处理它。

事件处理程序— React 不需要错误边界来从事件处理程序中发生的错误中恢复。如果我们想捕捉事件处理程序中的错误，我们可以在事件处理函数中使用通常的 try/catch 博客。

看看这个声明和使用错误边界的例子。

> “错误边界捕捉组件树中位于下方的组件中出现的错误，并且错误边界不能捕捉其自身内部的错误。在未能呈现错误消息的情况下，尝试呈现错误消息失败，错误将传播到其上最近的错误边界”

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **