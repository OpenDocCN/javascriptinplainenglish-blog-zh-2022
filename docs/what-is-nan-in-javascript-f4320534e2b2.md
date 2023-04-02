# JavaScript 中的 NaN 是什么？

> 原文：<https://javascript.plainenglish.io/what-is-nan-in-javascript-f4320534e2b2?source=collection_archive---------11----------------------->

## 在这篇博文中，我们将探讨 NaN 在 JavaScript 中的含义以及它出现的常见情况。

![](img/7edc5ecbd7350cf174e10de5431203ed.png)

Photo by [Christin Hume](https://unsplash.com/@christinhumephoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 开发人员经常会遇到 NaN 值。理解 NaN 的基本概念对于 JavaScript 开发人员来说非常重要，因为它使调试变得非常容易。在这篇博文中，我们将探讨 NaN 在 JavaScript 中的含义以及它出现的常见情况。

## 南简介

NaN 代表“非数字”，是全局对象的一个属性。它表示某个值不是合法的数字。当数学运算产生非数值时，返回 NaN。虽然这看起来很简单，但是 NaN 经常在 JavaScript 代码中意外出现。为了有效地调试代码，理解这种情况是如何发生的以及为什么会发生是很重要的。

有五种方法可以生成 NaN 值:

1.  将字符串解析为整数
2.  数学运算的结果不是一个实数
3.  操作使用 NaN
4.  该操作具有不确定的形式
5.  不是加法运算的字符串运算

下面几节将更详细地探讨这些情况。

## 将字符串解析为整数

生成 NaN 的一种常见方式是将字符串解析为整数。出现这种情况时，将返回 NaN 的值。

```
console.log(parseInt(“Hello world”)) //NaN
```

在第一个例子中，我们试图将字符串“two”解析成一个数字。因为这不是一个有效的数字，所以返回 NaN。在第二个例子中，我们试图将字符串“Hello world”解析成一个数字。这也不是一个有效的数字，因此再次返回 NaN。如果将字符串解析为数字，检查 NaN 值是很重要的。

## 数学运算的结果不是一个实数

生成 NaN 的另一种方式是当数学运算产生非实数时。例如，我们可以考虑一个例子，我们试图平方根一个负数。

```
console.log(Math.sqrt(-100)) //NaN
```

在这个例子中，我们取-100 的平方根。由于这不是一个实数，所以返回 NaN。

## 操作使用 NaN

生成 n an 值的另一种方式是当操作使用 NaN 时。

```
console.log(10 + NaN) //NaN
```

在这个例子中，我们将数字 10 加到 NaN 上。这会产生 NaN，因为 NaN 不是合法的数字。虽然我们通常不会直接将 NaN 传递到操作中，但是当您尝试对某个变量执行操作时，在代码早期导致 NaN 的变量可能会导致这个错误。

![](img/effc7836eba73867acf1649146c6d62d.png)

Photo by [Emmanuel Ikwuegbu](https://unsplash.com/@emmages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 该操作具有不确定的形式

生成 NaN 的另一种方式是当操作具有不定形式时。当一个操作有一个未知值时，这是一个可以生成 n an 的常见实例。例如，当我们试图添加未初始化的变量时，就会出现这种情况。

```
let x;console.log(x + 100) //NaN
```

在这个例子中，我们将未初始化的变量 x(未定义)加到数字 100 上。这导致了一种不确定的形式，因为我们不知道 x 值是多少。于是，楠就产生了。

## 不是加法运算的字符串运算

最后，当我们试图对字符串执行非加法运算时，也会产生 NaN。例如，如果我们尝试将一个字符串相乘，这将导致 NaN。

```
console.log(“Hello” * 2) //NaN
```

在本例中，我们尝试将字符串“Hello”乘以数字 2。由于这不是有效的操作，因此会生成 NaN。

## 结论

在这篇博文中，我们探讨了 JavaScript 中的 NaN 是什么，以及它是如何生成的。我们已经看到，NaN 可以以多种方式生成，并且可以出乎意料地出现。为了有效地调试代码，理解 NaN 是如何生成的非常重要。

我希望这篇文章澄清了任何困惑！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*