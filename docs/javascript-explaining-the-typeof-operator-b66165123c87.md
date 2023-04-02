# JavaScript:解释运算符的类型

> 原文：<https://javascript.plainenglish.io/javascript-explaining-the-typeof-operator-b66165123c87?source=collection_archive---------10----------------------->

## 由`typeof`操作符返回的不同值的含义，以及如何利用它们。

![](img/3e15f50375ae3c65f0d719799e9cd039.png)

Photo by [franco alva](https://unsplash.com/es/@franquito4133?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`typeof` 操作符是一个 JavaScript 操作符，用于确定操作数的类型。它返回一个对应于操作数类型的字符串。在这篇博文中，我们将讨论由`typeof`操作符返回的不同值的含义，以及如何利用它们。

## JavaScript 数据类型

首先，让我们回顾一下 JavaScript 支持的不同数据类型。有七种主要的数据类型被认为是原始的:

*   布尔代数学体系的
*   空
*   不明确的
*   数字
*   线
*   symbol(ECMAScript 2015 中的新功能)BigInt(ECMAScript 2020 中的新功能)
*   BigInt

这些基本类型是不可变的，这意味着它们的值不能改变。除了这些基本类型，JavaScript 还有一个引用类型。引用类型称为 Object，是一种复杂的数据类型。任何不是原始类型的东西都是对象。对象是可变的，这意味着它们的值可以改变。在 JavaScript 中，数组和函数都是对象。

## 运算符的类型

现在我们对 JavaScript 中的不同数据类型有了基本的了解，让我们更仔细地看看`typeof`操作符。`typeof` 操作符接受单个操作数，计算操作数的类型，并返回对应于该类型的字符串。

`typeof` 操作符的语法很简单，因为它只是关键字`typeof` 后跟操作数:

当您想要确定表达式的数据类型时，有一种替代语法利用括号。

上面的例子表明，如果没有括号，`typeof` 操作符将返回它遇到的第一个操作数的数据类型。在这种情况下，它是一个数字，因为操作数是变量 num，即 100。但是，当我们在表达式两边加括号时，它会返回表达式的数据类型，是一个字符串。这是因为由于类型强制，表达式`100 + ‘ hello’`的计算结果为`‘100 hello’`。

![](img/a79869e84d4ca34f60811f5feb5e1195.png)

Photo by [John Schnobrich](https://unsplash.com/@johnschno?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 简单的例子

下面的代码片段展示了对各种值使用`typeof` 操作符的结果。

有了这些例子，`typeof` 操作符看起来非常简单。但是，有些值可能会产生意想不到的结果。

## 类型的意外结果

**数组的类型:**

在 JavaScript 中，数组被认为是一种对象。因此，当您在数组上使用`typeof` 操作符时，它将返回‘object’。

```
typeof [0, false, “hello”] // ‘object’
```

**楠的类型:**

NaN 是一个表示非数字的值。在所有的数据类型中，你不会想到 NaN 会被归类为一个数字。然而，`typeof` 操作符返回 NaN 值的‘number’。

**空值的类型:**

在 JavaScript 中，`typeof` 操作符为空值返回“object”。这个 bug 源于 JavaScript 的早期。2015 年，提出了一个修复方案，但由于兼容性问题而被拒绝。

```
typeof null // ‘object’
```

**未声明变量的类型:**

如果你试图在一个没有声明的变量上使用`typeof` 操作符，它将返回‘undefined’。

```
typeof doesNotExist // ‘undefined’
```

## 结论

`typeof` 操作符是 JavaScript 中检查值的数据类型的强大工具。但是，有些值可能会产生意想不到的结果。意识到这些边缘情况很重要，因为它允许您能够利用`typeof` 操作符进行调试。

我希望这篇文章能消除你的任何困惑！祝你的编码面试好运！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。***