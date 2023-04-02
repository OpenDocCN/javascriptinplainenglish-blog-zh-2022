# RxJS 简介

> 原文：<https://javascript.plainenglish.io/introduction-to-rxjs-d04149065be0?source=collection_archive---------21----------------------->

## [RxJS](https://medium.com/@lorenzozar/list/rxjs-39bc4f4110ec)

## RxJS 代表 JavaScript 的反应式扩展。

![](img/12a3f0b2ea2d9b5e21355ee47519fe59.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Reactive Extensions 库最初是由微软开发的，从那时起，它已经被用于其他几种语言，如 Java (RxJava)和 Python (RxPy)。

# RxJS 是什么？

根据[官方文档](https://rxjs.dev/guide/overview)，“ *RxJS 是一个利用可观察序列*组成异步的、基于事件的程序的库”。

换句话说，RxJS 是一个帮助我们管理和操作数据的库。

# 让我们举个例子

举个例子，让我们想想加工桃子！

![](img/b5658ba70afd7ea40136616b92bf3e77.png)

What is RxJS if not a stream of peaches?

传送带上的桃子产生了一连串的桃子。我们不知道一段时间后会有多少桃子，也不知道它们什么时候会停掉。然而，我们可能想要对那些桃子做一些操作。举个例子，

*   把好的从坏的中过滤出来，
*   将其中一些转化成果汁
*   把一些桃子和其他水果混合在一起
*   给一些桃子贴上标签出售

在 RxJS 的世界里，桃子是我们可能想要操纵的数据。简单来说，一个数据流叫做可观测流。

我们不知道在一段时间内会收到多少“数据”，也不知道何时会停止接收数据。然而，RxJS 提供了大量的操作符来操作数据。

我们将在后面解释可观测量和其他 RxJS 术语。目前，理解 RxJS 是一个操作数据流的库是很重要的。

# 为什么我们需要 RxJS 来操作数据？

简而言之，我们可以说这个库与传统技术如 Promises 或 async/await 相比有几个优点。

特别是，RxJS 可以随着时间的推移产生多个值，并且它使用推送模型在特定事件发生时通知应用程序。这是反应式编程的核心。

此外，与承诺不同，在异步操作终止之前取消它们是可能的。

我们将讨论[为什么我们需要 RxJS？在下一篇文章中有更多的细节。](https://www.vitainbeta.org/2022/01/25/why-rxjs-rxjs-vs-promises/)

# 什么是反应式编程？

你可以找到很多反应式编程的定义。从理论的角度来看， [Wikipedia](https://en.wikipedia.org/wiki/Reactive_programming) 将反应式编程定义为“*一种关注数据流和变化传播的声明式编程范例*”。

换句话说，反应式编程就是用异步数据流编程。任何东西都可以是流:变量、用户输入、数据结构等等。因此，听其自然，做出适当的反应是可能的。

当我们将函数范式与反应式编程相结合时，我们希望在声明值时动态地指定它们的行为。

感谢 [RxJS 操作符](https://rxjs.dev/guide/operators)，我们得到了一套合并、过滤和操作数据流的工具。

# 要点

*   RxJS 是一个随时间处理数据的库
*   相对于传统技术的一些优势包括随着时间产生多个值的可能性和取消异步操作
*   反应式编程是用异步数据流编程。

接下来:[为什么是 RxJS？RxJS vs 承诺](https://medium.com/p/b28962771d68)