# JavaScript:真就是假？

> 原文：<https://javascript.plainenglish.io/javascript-true-is-false-a24674664223?source=collection_archive---------17----------------------->

![](img/9b0fd6a0b3c38bf832a12a68fb6f9e50.png)

Photo by [Magnet.me](https://unsplash.com/@magnetme?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

虽然 JavaScript 是一种流行而强大的编程语言，但它以可疑的设计决策和混乱的行为而闻名。在本文中，我们将研究一个场景，在这个场景中，JavaScript 在使用双爆炸运算符比较字符串时表现出不直观的行为。

## 真就是假

让我们来看看下面的例子，它使用了两个 bang 运算符来比较两个字符串。

在这个例子中，结果似乎完全不直观。两个完全不同的字符串，对它们执行相同的操作，并以某种方式导致彼此相等。

这种行为的原因是，当使用双爆炸运算符时，JavaScript 将字符串强制转换为布尔值。在 JavaScript 中，空字符串、0、null、undefined 和 NaN 都被强制为 false。任何其他值都被强制为 true。因此，当我们在字符串“false”和“true”上使用双爆炸运算符时，它们都被强制转换为布尔值并变为 true。

我们可以通过下面的例子来证实这一点。

在这个例子中，我们使用布尔构造函数显式地将字符串强制转换为布尔值。我们可以看到，结果和以前一样。

这种行为可能会令人困惑，并在我们的代码中导致意外的结果。在 JavaScript 中处理字符串时，了解这种行为很重要。

## 结论

在本文中，我们研究了 JavaScript 中一个不直观的场景，其中两个完全不同的字符串看起来是相等的。我们分解了 double bang 操作符的行为，并看到了它如何在我们的代码中导致意想不到的结果。

我希望这篇文章有助于澄清任何困惑，并帮助您避免自己代码中的任何潜在问题。感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***