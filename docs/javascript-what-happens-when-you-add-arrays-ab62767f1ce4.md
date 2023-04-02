# JavaScript:当你添加数组时会发生什么？

> 原文：<https://javascript.plainenglish.io/javascript-what-happens-when-you-add-arrays-ab62767f1ce4?source=collection_archive---------14----------------------->

## 探索当两个数组相加时会发生什么。

![](img/936f6c9d6f52a2c2ad7ad4122c3e7abe.png)

Photo by [Scott Graham](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您曾经在 JavaScript 中使用过数组，您可能想知道当您将数组加在一起时会发生什么。在本文中，我们将探讨这个问题，并研究当我们将两个数组相加时会发生什么。

## 添加数组

当我们在 JavaScript 中将两个数组加在一起时，结果非常不直观。当我们把两个数组加在一起时，我们希望发生两件事。要么将两个数组连接成一个数组，要么将数组的元素相加。然而，从下面的例子中，我们可以看到这两种情况都没有发生。

JavaScript 实际上没有为数组定义“+”操作符。因此，当我们试图将两个数组加在一起时，JavaScript 会将数组强制转换成字符串并连接起来。我们可以分解上面例子中发生的事情。

首先，JavaScript 将第一个数组强制转换成一个字符串。然后，它将第二个数组强制转换为字符串。最后，它将两个字符串连接在一起。这就是为什么两个数组相加的结果是一个字符串而不是一个数组。

## 结论

在本文中，我们探讨了在 JavaScript 中将两个数组相加会发生什么。我们看到结果是一个字符串而不是一个数组。我们检查了这个功能，并确定这是因为没有为数组定义“+”运算符。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***