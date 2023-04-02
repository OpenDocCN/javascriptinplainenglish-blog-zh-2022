# 反应最佳实践

> 原文：<https://javascript.plainenglish.io/reactjs-best-practices-ec6bc148e6f5?source=collection_archive---------4----------------------->

## 如何充分利用 React 库，以及应该采取什么步骤。

React 是最受欢迎的 JavaScript 前端库之一。它提供了许多伟大的功能，但正如我们所知，一切都有利弊。如果你不知道如何正确地使用任何技术，而不是简化事情，它会使整个事情变得复杂。

![](img/e4e0d0c733138ed4c8b9ea0310d01364.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将讨论如何充分利用 React 库，以及应该采取什么步骤。我们开始吧

1.  ***组件要有单一的职责*** ，不要创建直接渲染很多东西的大型组件。这使得组件很难维护，并且阻碍了 React 的优化，因为它必须创建一堆元素并计算差异。
2.  **中的*分开应用状态逻辑和*中的**不同组件。
3.  ***通过仅在必要时声明状态*** 来最小化状态的使用。
4.  试着 ***利用钩子*** 。参考给定的链接，了解如何适应它[https://reactjs.org/docs/hooks-intro.html](https://reactjs.org/docs/hooks-intro.html)
5.  ***可以使用 React.useMemo 或者 React.useCallback 进行性能优化。*** 但是考虑一下，React.memo 应该只适用于纯组件。**你不应该在没有测量**的情况下使用 React.useMemo 和 React.useCallback **，因为这些优化是有代价的，你必须确定成本和收益，这样你才能决定它实际上是否有益。**
6.  ***使用按键道具，*** 按键帮助反应识别哪些物品被修改，被添加，或者被删除。更多细节请参考此图[https://reactjs.org/docs/lists-and-keys.html](https://reactjs.org/docs/lists-and-keys.html)
7.  ***避免使用索引*** 或任何重复值作为关键属性。
8.  在添加额外的库之前，了解一下 react 提供的内置特性。你可以构建一个完整的应用程序，而不包含任何其他的库。
9.  为了避免应用程序中的内存泄漏，

*   如果可能的话 ***在从组件中移出之前清除所有订阅*** (API 请求、事件监听器、定时器)。
*   ***更新组件状态前，检查组件是否在 DOM*** 中，然后更新状态。

10. ***写测试*** 因为测试保证了代码的完整性。更多详情请参考给定链接【https://reactjs.org/docs/testing.html 

我在这里列出了一些实践，以后还会添加更多。请在评论中让我知道你在编写任何 react 应用程序时遵循的准则。

我希望这有所帮助。一定要评论和分享，让我知道你是否喜欢它，你的小小努力鼓励我写更多。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**