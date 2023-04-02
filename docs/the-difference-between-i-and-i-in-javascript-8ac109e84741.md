# JavaScript 中 i++和++i 的区别

> 原文：<https://javascript.plainenglish.io/the-difference-between-i-and-i-in-javascript-8ac109e84741?source=collection_archive---------5----------------------->

## 探索后缀和前缀运算符之间的区别。

![](img/8168a058b5ff88c7fa5b929a19281a7b.png)

Photo by [Hatice Yardım](https://unsplash.com/@haticehuma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，可以使用 `i++`或`++i`增加一个值。这两个操作符都将变量的值增加 1，但它们的做法略有不同。开发人员经常混淆这两个操作符之间的区别，导致他们的代码出现错误。在本文中，我们将探讨这两个操作符之间的区别。

## 后缀运算符

`i++`被称为后缀运算符。这意味着变量的值在表达式中使用后会递增。例如，考虑以下代码:

```
let i = 0;console.log(i++); // Prints 0console.log(i); // Prints 1
```

## 前缀运算符

`++i`称为前缀运算符。这意味着变量的值在表达式中使用之前是递增的。例如，考虑以下代码:

```
let i = 0;console.log(++i); // Prints 1console.log(i); // Prints 1
```

如您所见，当我们使用`++i`操作符时，I 的值在用于表达式之前是递增的。

## 理解差异

虽然您现在可能能够预测这些操作符的输出，但是真正理解为什么会产生输出是很重要的。变量递增和返回的顺序在前缀和后缀运算符之间是不同的。

使用后缀运算符时，变量的值首先在表达式中使用，然后递增。这意味着如果我们增加一个变量，然后把它打印出来，我们会看到原来的值。

另一方面，使用前缀运算符时，变量的值首先递增，然后在表达式中使用。这意味着当我们使用前缀运算符时，我们使用的是变量递增后的新值。

## 结论

为了避免代码中的混乱和错误，理解这两个运算符之间的区别是很重要的。总之，后缀运算符将首先在表达式中使用变量，然后递增它，而前缀运算符将首先递增变量，然后在表达式中使用它。

我希望这篇文章能消除你的任何困惑。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*