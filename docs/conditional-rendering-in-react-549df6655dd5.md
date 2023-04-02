# React 中的条件渲染

> 原文：<https://javascript.plainenglish.io/conditional-rendering-in-react-549df6655dd5?source=collection_archive---------10----------------------->

## 关于如何在 React 中使用条件渲染的简短教程。

![](img/03e8706b4d40e8ae3f5badaf05c1d659.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是条件渲染？

React 中的条件渲染是一种基于特定条件显示组件或元素的方式。它的工作原理和普通 Javascript 中的条件一样。我们可以使用 Javascript 操作符，比如 if 语句和三元操作符来决定什么将被呈现给 UI。

# 如何在 React 中使用条件渲染

在 React 中，我们可以选择几种方法来实现条件渲染。最常见的方式是`if`语句、`&&`运算符和三元运算符。一种方法可能比另一种更适合你，这取决于你的条件和/或偏好。

我们将利用这个应用程序组件来帮助演示在 React 中实现条件渲染的不同方式。

## 如果语句

当您必须在要显示的两个或更多不同元素或组件之间做出决定时，您可能希望使用 if，else 语句。

这是一种基于值`isLoggedIn`呈现元素的简单方法。与其他方式相比，它包含更多的代码行，但它仍然工作得很好。但是需要注意的是，你不能在你的组件的渲染和 JSX 部分使用一个`if`语句。

## 三元运算符

React 中的三元运算符是在要呈现的两个选项之间做出决定的一种更常见的方式。

就像`if`语句一样，这将检查`isLoggedIn` 的计算结果是否为真，然后根据其值呈现正确的元素。与`if`语句不同，它可以在 JSX 内部使用，并且只占用一行代码！

## &&运算符

常规 Javascript 中的逻辑运算符`&&`对您来说可能很熟悉。在 Javascript 中，它通常出现在`if`语句中。它将检查多个条件是否为真，并在两个条件都为真或真时运行`if`块中的代码。

在 React 中，当我们有一个条件需要评估为 true 以便将元素呈现到 UI 时，我们可以利用这一点。

在这个例子中，只有当我们在`mail`数组中包含多个项目时，我们的`h1`才会显示。它将检查左边的条件，然后检查右边的元素。在这种情况下，两者都将评估为真，因为我们的状态在数组中包含不止一个项目，并且`h1`元素将始终为真。

# 结论

在本文中，我们讨论了什么是条件渲染，以及如何以 React 中最常见的方式实现它。还有其他几种实现条件渲染的方法，比如使用 [switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch) 语句和 [IFFEs](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) 语句，但是这里我们学习了它更常见的用法。

在 React 中使用和理解条件渲染非常重要，因为您可能会在 React 组件中经常看到它的使用。

要了解这个概念的更多信息，请阅读关于[条件渲染](https://reactjs.org/docs/conditional-rendering.html)的 React 文档。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***