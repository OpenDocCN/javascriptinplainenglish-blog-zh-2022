# JavaScript:使用 at()方法进行负索引

> 原文：<https://javascript.plainenglish.io/javascript-negative-indexing-with-the-at-method-9bc72c3bb903?source=collection_archive---------7----------------------->

## `at()`方法为开发人员提供了访问负索引(`arr[arr.length — 1]`)的旧方法的替代品。

![](img/8ccc1eecb00408c42551be9057cc6e09.png)

Photo by [Lala Azizli](https://unsplash.com/@lazizli?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 引入了一种方法来轻松访问数组和字符串的结束值。`at()`方法为开发人员提供了访问负索引(`arr[arr.length — 1]`)的旧方法的替代品。

## at()方法的动机

在 JavaScript 中，开发人员经常需要访问数组或字符串的最后一个值。例如，如果您有一个用户数组，您可能想要访问最后添加的用户。当试图完成这项任务时，开发人员发现 JavaScript 没有 Python 那样的支持，Python 提供负索引(`arr[-1]`)。在过去，开发人员会通过使用括号符号及其长度来访问数组的最后一个索引。

这种访问最后一个索引的方式是可行的，但是不方便，并且不是最直观的访问数据的方式。JavaScript 引入了`at()`方法来简化这个过程。

## 句法

`at()`方法只需要一个参数。此参数是您要访问的元素的索引。该方法允许参数为正和负。如果参数为负，则该方法将从数组中的最后一项开始计数。如果在提供的索引处没有值，方法将返回未定义。

正如我们所看到的，`at()`方法使得访问数组中的最后一项变得更加简单。

![](img/83d36fd4322cea0c799ae2a9c2e270ef.png)

Photo by [Luke Southern](https://unsplash.com/@lukesouthern?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 小数

如果您为`at()`方法提供一个十进制值，参数将截断为 0。这意味着小数将被删除，只使用数字的整数部分。

这非常有用，因为它为开发人员提供了一种通过索引随机选择元素的简单方法。

## 结论

`at()`方法是一个非常有用的工具，它使得在 JavaScript 中处理数组和字符串变得更加容易。它的语法很简单，并且为开发人员提供了一种访问数据的简单方法。

我希望这篇文章能教会你一些东西！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***