# JavaScript:如何用 Array.reduce()填充对象

> 原文：<https://javascript.plainenglish.io/javascript-how-to-populate-an-object-with-array-reduce-6faa8eb947d0?source=collection_archive---------14----------------------->

## 关于如何使用 Array.reduce()在 JavaScript 中填充对象的教程。

![](img/cf3614580dfa30a5998f2771398764ce.png)

Photo by [Malte Helmhold](https://unsplash.com/@maltehelmhold?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`Array.reduce()`是一个非常强大的方法。其独特的功能允许您以灵活的方式使用该方法。在本文中，我们将讨论如何使用`Array.reduce()`来填充一个对象。

## Array.reduce()简介

`reduce()`方法允许你将一个数组缩减为一个值。`reduce()`方法有两个参数:一个回调函数和一个可选的初始值。为数组中的每个元素调用回调函数。回调函数的返回值被用作“累加器”。累加器是由`reduce()`返回的值。

回调函数接受两个参数:累加器和当前值。当前值是回调函数当前正在处理的元素的值。

如果你提供一个初始值作为`reduce()`的第二个参数，这个初始值将作为累加器的初始值。如果不提供初始值，数组的第一个元素将用作累加器的初始值。

![](img/61292f073ab9d341e0349ab604869c27.png)

Photo by [Vadim Bozhko](https://unsplash.com/@bozhstudio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 利用 Array.reduce()填充对象

如果您曾经需要将一组数据转换成一个对象，您会知道这可能有点棘手。然而，`Array.reduce()`非常灵活，它的初始值可以为我们所用。

我们可以通过下面的例子来观察这种功能。假设我们有一个元素数组，表示杂货店购物车中的商品。

如果我们想将这个数组转换成一个对象，其中键是数组中的条目，值是条目的相应数量，我们可以如下使用`Array.reduce()`:

在上面的代码中，我们为`reduce()`方法提供了一个空对象的初始值。这个对象将被用作累加器的初始值。我们还定义了一个接受两个参数的回调函数:累加器(`acc`)和当前值(`cur`)。回调函数首先检查当前键是否存在于累加器对象中。如果该键不存在，则将其添加到值为 0 的累加器对象中。否则，该项的值增加 1。最后，回调函数返回累加器对象。

## 结论

在本文中，我们讨论了如何使用`Array.reduce()`来填充一个对象。我们也看到了初始值是如何为我们所用的。`Array.reduce()`是一个非常强大的方法，可以以多种方式使用。

希望这篇文章教会你一些东西！祝你的编码面试好运！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***