# JavaScript For 循环与 For Each:解释区别

> 原文：<https://javascript.plainenglish.io/javascript-for-loops-vs-for-each-the-difference-explained-39a1378f14d7?source=collection_archive---------8----------------------->

## 了解 for 循环和 for each 循环的区别，以便正确使用它们。

![](img/82d41aed3fc2a957c6bdb64f4207c1fe.png)

Photo by [Avel Chuklanov](https://unsplash.com/@chuklanov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当您第一次学习 JavaScript 时，区分 for 循环和 forEach 可能会很混乱。它们似乎都在做同样的事情——遍历数组或数据列表。但是，为了有效地使用这两种方法，您需要了解它们之间的一些关键区别。在本文中，我们将解释 for 循环和 for each 循环的区别，并向您展示如何正确使用它们！

## 句法

for 循环和 forEach 之间第一个也是最明显的区别是语法。传统的 for 循环如下所示:

只要条件(I 小于数组的长度)为真，这段代码就会运行循环。在 for 循环中，可以使用索引“I”来访问数组的每个元素。

另一方面，forEach 方法看起来像这样:

这段代码将遍历数组的每个元素并执行给定的操作。forEach 语法更短，更容易阅读，这也是一些开发人员更喜欢它的原因。

## 表演

for 循环和 forEach 的另一个关键区别是性能。For 循环通常比 forEach 快，因为它们没有为每个元素调用函数的开销。然而，这种差异通常可以忽略不计，除非您正在处理非常大的数组。

![](img/da7384652c767ac43634791af4f43630.png)

Photo by [Green Chameleon](https://unsplash.com/@craftedbygc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## forEach 的警告

对 forEach 的一个警告是，你不能过早地跳出循环。这意味着，如果您需要在循环到达末尾之前停止循环，您将不得不使用传统的 for 循环。

forEach 的另一个警告是它不支持返回值。例如，如果您想遍历一个数组，并且您想返回以字母“A”开头的第一个元素，那么您不能用 forEach 做到这一点。这意味着如果需要从循环中返回值，就必须使用传统的 for 循环。

使用 await 关键字时，forEach 方法可能会导致不正确的输出。forEach 方法不是为处理异步代码而构建的。这意味着，如果在 forEach 方法中有一个异步函数，代码可能不会以期望的顺序或方式执行。

## 结论

forEach 方法更容易读写。它可以与箭头函数一起使用，使代码更加简洁。然而，尽管 forEach 方法很方便，但它也存在一些问题。理解何时使用 forEach 方法以及何时使用传统的 for 循环非常重要。

我希望这篇文章能消除你的任何困惑。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**