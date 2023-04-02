# JavaScript:双爆炸操作符(！！)

> 原文：<https://javascript.plainenglish.io/javascript-the-double-bang-operator-3dcdd21f8a29?source=collection_archive---------1----------------------->

## 什么双爆炸(！！)运算符是什么以及如何在代码中使用它

![](img/5fb2948fe5b2929f51301f1dacce6184.png)

Photo by [Lala Azizli](https://unsplash.com/@lazizli?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种强大的语言，可以做一些令人惊奇的事情。JavaScript 最酷的特性之一是双击操作符。该运算符允许您返回操作数的相关布尔值。在本文中，我们将看看什么是双爆炸操作符，以及如何在代码中使用它。

## JavaScript 中的布尔值

在 JavaScript 中，每个值都有一个相关的布尔值。这个布尔值由所谓的值的“真实性”决定。“真”值是在转换为布尔值时评估为真的值。相反，“假”值是指在转换为布尔值时计算结果为假的值。

## JavaScript 中的假值和真值

在 JavaScript 中，有六个值被认为是错误的:

*   `false`
*   `0`
*   `“”`(空弦)
*   `null`
*   `undefined`
*   `NaN` (非数字)

JavaScript 中的真值是任何不为假的值。值得注意的是，在 JavaScript 中，空数组或空对象都被认为是真值。

![](img/cbf16e5334636cc3b23e737a2c7fece6.png)

Photo by [Scott Graham](https://unsplash.com/es/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 双爆炸运算符(！！)

双爆炸运算符是一种强制将值转换为其布尔等效值的方法。为了理解双爆炸算子是如何工作的，我们需要考虑单爆炸算子的功能。单爆炸运算符用于反转操作数的布尔值。因此，如果一个值为真，单爆炸运算符将返回假。如果值为 falsy，单爆炸运算符将返回 true。

使用双爆炸操作器将两次利用单爆炸操作器的反转功能。因此，当您对一个值使用双爆炸运算符时，您实际上是在说“将该值转换为布尔值，并返回布尔值的等价物”。

## 应用

double bang 运算符是一种将值转换为布尔等效值的有效而简洁的方法。当您需要检查一个值是真还是假时，这可能很有用。这种情况在 web 开发中很普遍，尤其是当您需要仅在满足特定条件的情况下呈现组件时。

## 结论

double bang 操作符是每个 JavaScript 开发人员都应该熟悉的强大工具。在本文中，我们已经了解了什么是 double bang 操作符，以及如何在代码中使用它。希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***