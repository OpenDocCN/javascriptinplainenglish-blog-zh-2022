# 为什么我们可以改变用“const”初始化的 JavaScript 对象

> 原文：<https://javascript.plainenglish.io/why-we-can-mutate-a-javascript-object-initialized-with-const-b4ef5d9c0070?source=collection_archive---------9----------------------->

## 本文研究了为什么我们可以改变用“const”初始化的 JavaScript 对象，以及什么时候这样做比较合适。

![](img/1463b673b011d5167c00f492769bb2f5.png)

Photo by [Alexandra Fuller](https://unsplash.com/@alexandrajf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您可能想知道为什么可以改变用关键字`const`初始化的 JavaScript 对象。毕竟，`const`应该是创建一个常量值，对吗？这是一个关于`const` 关键词的常见误解。在本文中，我们将看看为什么我们可以改变用`const`初始化的 JavaScript 对象，以及什么时候这样做是合适的。

## 参考值

JavaScript 中的引用值指向内存中存储该值的位置。对象是引用值，这意味着当你把一个对象赋给一个变量时，你实际上是在给那个对象赋一个引用。我们能够改变 JavaScript 对象，因为在 JavaScript 中对象是通过引用传递的。

## const 的功能

当你使用`const`时，你实际上并没有创建一个不可变的对象。您正在创建对该值的常量引用。这意味着你不能重新分配用`const`声明的变量，但是你可以改变对象本身。下面的代码片段演示了这项功能。

如您所见，我们能够改变对象本身，因为我们没有将 obj 变量重新分配给不同的引用值。关键字`const` 阻止重新分配，但不阻止变异。

![](img/d794fb52044b682f4ce83f2e48bc136a.png)

Photo by [Anthony Riera](https://unsplash.com/@frenchriera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 何时使用 const vs. let

既然我们知道可以改变用`const`声明的对象，那么我们应该什么时候使用`const`？一般来说，当你计划不再重新分配变量时，你应该使用`const` 。这将有助于防止意外重新分配可能导致的任何错误。如果你计划改变对象，那么使用`const` 就可以了。

有些情况下，你可能想重新分配用`const`声明的变量。在这些情况下，您可以使用`let` 关键字来代替。

使用`let` 关键字时，您可以重新分配对象的参考值，这与`const` 关键字不同。

## 结论

我们可以改变用`const` 声明的 JavaScript 对象，因为在 JavaScript 中对象是通过引用传递的。当决定是使用`const` 还是`let`时，如果你不打算重新分配变量，你应该使用`const` 。如果你计划重新分配变量，那么使用`let` 是合适的。

我希望这篇文章有助于澄清 JavaScript 中关于`const` 关键字的任何困惑。祝你的编码面试好运！

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*