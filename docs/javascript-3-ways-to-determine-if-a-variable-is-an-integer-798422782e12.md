# JavaScript:确定变量是否为整数的 3 种方法

> 原文：<https://javascript.plainenglish.io/javascript-3-ways-to-determine-if-a-variable-is-an-integer-798422782e12?source=collection_archive---------12----------------------->

## 三种最常见的方法:`Number.isInteger()`，检查余数，利用严格的等式操作符和 parseInt。

![](img/fb514f6e45d5844f19db53306c754036.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，有很多方法可以确定一个变量是否是整数。在本文中，我们将讨论三种最常见的方法:`Number.isInteger()`，检查余数，以及利用严格的等式运算符和 parseInt。我们还将提供如何使用每种方法的例子。

## Number.isInteger()

`Number.isInteger()`方法是检查变量是否为整数的最直接的方法。该方法确定传入的值是否为整数。此方法返回一个布尔值，如果传入的值是整数，则为 true，否则为 false。值得注意的是，对于可以用整数表示的浮点数，该方法将返回 true。

## 检查剩余部分

检查变量是否为整数的另一种方法是检查余数。这可以通过使用模数运算符来实现，该运算符返回除法运算的余数。如果余数是 0，那么我们知道这个数是一个整数。

然而，使用这种方法有一些注意事项。如果传递给函数的值是空字符串或布尔值，函数将返回 true。为了避免这种不直观的功能，我们可以检查传入的值是否是数字类型。

![](img/ebc55b9cbc44fdfd9f7e93e0d86cc67a.png)

Photo by [Kyle Gregory Devaras](https://unsplash.com/@kyledevaras?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 利用严格的相等运算符和 parseInt

我们将介绍的最后一种方法涉及到利用严格的等式操作符和 parseInt。严格相等运算符`===`检查两个值在值和类型上是否相等。同时，parseInt 试图将一个值解析成一个整数。因此，通过使用这两个运算符，我们可以检查变量是否是整数。

## 结论

总之，在 JavaScript 中有多种方法可以检查变量是否是整数。最直接的方法是利用`Number.isInteger()`法。然而，所有这些方法都有一些注意事项和优点，在您的代码中使用它们之前，了解这些是很重要的。

希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*