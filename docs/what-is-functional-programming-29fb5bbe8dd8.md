# 什么是函数式编程？

> 原文：<https://javascript.plainenglish.io/what-is-functional-programming-29fb5bbe8dd8?source=collection_archive---------9----------------------->

## 什么是函数式编程，以及它如何帮助您编写更好的代码。

![](img/7360d86f130c557142247226311c7c90.png)

Photo by [Mr. Bochelly](https://unsplash.com/@bochelly?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

函数式编程是一种编程范式，将计算视为数学函数的求值，避免改变状态。它在过去几年里变得流行起来，部分原因是它在网络上的使用越来越多。特别是 JavaScript 开发人员，他们通常遵循一种函数式编程方法，这种方法既可以在 web 应用程序的前端使用，也可以在后端使用。

在本文中，我们将探索什么是函数式编程，以及它如何帮助您编写更好的代码。我们还将看看使用函数式编程带来的一些好处，以及一些缺点。最后，我们将快速浏览一下目前使用的一些最流行的函数式语言。

## 函数式编程简介

函数式编程是一种将函数视为一等公民的编程风格。这意味着函数可以赋给变量，作为参数传递给其他函数，以及从函数返回。此外，函数式编程通常避免改变状态，使代码更容易调试。

函数式编程围绕着创建纯函数。纯函数是这样的函数，给定相同的输入，将总是返回相同的输出，并且没有副作用。这意味着该函数不会改变任何数据，也不会读取或写入任何外部数据源。纯函数很容易测试和推理，因为它们没有副作用。

函数式编程起源于 20 世纪 50 年代，伴随着 lambda 演算的发展，lambda 演算是一种描述计算的正式系统。然而，直到 20 世纪 70 年代末，约翰·巴科斯发表了他的论文“编程可以从冯·诺依曼风格中解放出来吗？”在这篇论文中，Backus 认为函数式编程可以提高程序员的生产率和软件质量。

尽管 Backus 尽了最大努力，函数式编程直到 21 世纪初才真正起飞，当时几种函数式语言——包括 Haskell、OCaml 和 Lisp——在研究人员和开发人员中流行起来。近年来，由于函数式编程在 web 上的使用越来越多，人们对函数式编程的兴趣重新高涨。

![](img/60e60e5484b6c2e7bbaa0b71cebfa38a.png)

Photo by [Lauren Mancke](https://unsplash.com/@laurenmancke?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 函数式编程的好处

使用函数式编程有几个好处:

**更容易推理和调试**:因为函数式编程避免了改变状态，所以函数更容易调试。这是因为当你试图理解一个函数是如何工作的时候，你需要跟踪的东西更少了。此外，许多函数式编程语言都包含类似类型推断和模式匹配的特性，这使得查找代码中的错误变得更加容易。

**简洁的代码**:函数式编程往往会产生更简洁的代码。这是因为函数通常很小，每个函数都有特定的用途。这些职能遵循单一责任原则，即一个职能应该只有一个目的。这使得理解和维护代码变得更加容易。

**可并行化**:函数式编程通常比命令式编程更具并行性。这是因为功能代码是由可以并行执行的小而独立的功能组成的。相比之下，命令式代码通常依赖于共享状态，这使得并行化更加困难。

**更好的可扩展性**:很多人认为函数式编程比传统的命令式编程语言更适合大规模系统。这是因为函数式程序由于依赖于不可变的数据结构和纯函数而具有更强的可伸缩性。

![](img/cc55a47345147dcde6d9442ee873c39f.png)

Photo by [Avel Chuklanov](https://unsplash.com/@chuklanov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 函数式编程与面向对象编程

函数式编程和面向对象编程是两种不同的编程方法。它们有不同的优点和缺点，并且通常用于不同的目的。

面向对象编程是一种依赖于对象或包含数据和方法的数据结构的编程风格。这种编程风格通常用于创建可重用的代码。此外，面向对象的编程通常更容易对现实世界的现象进行建模。

另一方面，函数式编程是一种依赖于函数的编程风格。这些函数接受输入并返回输出，但是它们不改变状态。这使得函数代码更容易推理和调试。此外，函数式编程通常会产生更简洁的代码。

## 结论

在比较函数式编程和面向对象编程时，开发人员经常想知道哪种编程范式更好。答案取决于你的需求。如果您正在寻找易于推理和调试的代码，那么函数式编程可能是更好的选择。然而，如果您正在寻找更容易重用的代码，那么面向对象编程可能是更好的选择。最终，这两种编程模式都有各自的优点和缺点，因此选择最适合您项目的模式非常重要。

希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***