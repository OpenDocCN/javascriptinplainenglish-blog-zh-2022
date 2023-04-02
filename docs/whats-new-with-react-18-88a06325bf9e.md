# React 18 有什么新功能？

> 原文：<https://javascript.plainenglish.io/whats-new-with-react-18-88a06325bf9e?source=collection_archive---------11----------------------->

![](img/6b2064e34bc3d70ca2087f9100298310.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

有了批处理、并发、转换 API 和更多功能，React 18 看起来很有前途。每发布一个新版本，框架就变得越来越好。最常用的 JavaScript 框架， [React 是最常用于构建具有大量不可思议特性的现代应用程序的框架。](https://www.technologysage.com/advantages-of-developing-modern-web-apps-with-react)

React 的团队宣布了版本 18 的发布计划。成立了一个工作组，让社区做好准备，逐渐适应新的功能。下一个 React 版本中有许多 API 变化和重要特性。

# 新功能和变化

## **1。新的根 API**

为了跟踪树的渲染，“根”是指向 React 使用的数据结构级别的指针。此外，API 遗留系统中的根对用户来说是不透明的，因为他们将它附加到 DOM 元素上，并使用 DOM node 访问它，而不向用户公开它。然而，根节点不需要存储到 DOM 节点。

对于正在运行的更新有一些担心，包括需要不断地将容器传递到渲染中，即使它保持不变。新增的根 API 解决了这个问题，因此不再需要将容器传递到呈现中。此外，根 API 更改允许删除水合物方法，并用根选项替换它。

## **2。新开始转换 API**

这使应用程序保持响应。这是最重要的更新之一，它使应用程序在大屏幕更新期间保持响应。此外，API 使用户能够控制并发性，从而促进用户交互。这是通过将繁重的更新包装为“开始转换”来完成的，只有当有更紧急的更新启动时才会被中断。

因此，它实际上对缓慢更新和紧急更新进行了分类。如果用户操作中断了过渡，React 会丢弃未完成的陈旧渲染工作，只渲染最新的更新。

## **3。自动配料增强功能**

批处理只不过是将 React 的多个状态更新组合成一个呈现状态，以实现更好的计算性能。在早期的 React 版本中，批处理只针对 React 事件处理程序。但是，对于任何其他事件，如设置超时、承诺内的更新、异步状态更新、设置超时和本机事件处理程序，在 React 中默认情况下不会对更新进行批处理。

这可以通过在版本 18 中使用 Root API 添加自动批处理来解决。所有更新都将被自动批量处理，不管它们来自何处。

## **4。架构改进，新悬念 SSR**

通过 React 18 的服务器端渲染，增加了一个架构增强。此外，服务器端呈现从服务器上的 React 组件生成 HTML，并将其返回给客户端。现在，客户机能够在 JavaScript 的捆绑包加载和运行之前看到页面的内容。

然而，SSR 有一个缺点。它不允许组件等待数据。这意味着在 HTML 呈现给客户机之前，应该为服务器组件准备好数据。你还需要等待所有的成分被水合，然后才能与它们相互作用。

这个问题可以通过悬念的两个新功能来解决，如选择性水合和流式 HTML。

# 包扎

React 18 包括现成的增强功能和有影响力的新功能。此外，它为新的 React 应用程序开发可能性扫清了道路。

新版本将带来许多强大的功能来提升开发人员的体验，并有助于创造惊人的网络体验。它开启了新的可能性并提升了性能。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*