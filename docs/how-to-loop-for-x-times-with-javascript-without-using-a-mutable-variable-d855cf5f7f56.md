# 如何在不使用可变变量的情况下用 JavaScript 循环 x 次？

> 原文：<https://javascript.plainenglish.io/how-to-loop-for-x-times-with-javascript-without-using-a-mutable-variable-d855cf5f7f56?source=collection_archive---------1----------------------->

![](img/b6ec656aa8f8f8a68833a0fbdab428eb.png)

Photo by [Jen Theodore](https://unsplash.com/@jentheodore?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 重复运行代码`x`次，而不使用可变变量。

在本文中，我们将看看如何在不使用可变变量的情况下用 JavaScript 重复运行代码`x`次。

# 使用数组构造函数、扩展运算符和 Array.prototype.map

我们可以用`Array`构造函数创建一个长度为`x`的数组，然后调用`map`方法返回我们想要的结果。

例如，我们可以写:

```
const res = [...Array(10)].map((_, i) => {
  return i * 10;
});
console.log(res)
```

我们用`Array(10)`创建一个有 10 个空槽的数组。

然后我们将它扩展到一个新的数组中，然后我们调用`map`来返回数组中我们想要的元素。

我们得到索引`i`，乘以 10 并返回。

因此，`res`是:

```
[0, 10, 20, 30, 40, 50, 60, 70, 80, 90]
```

# 使用数组构造函数、扩展运算符和 Array.prototype.forEach

如果我们不想在重复运行我们的代码后返回一个新的数组，我们也可以在空数组上调用`forEach`方法来代替`map`。

例如，我们可以写:

```
[...Array(10)].forEach((_, i) => {
  console.log(i);
});
```

我们只是在`forEach`回调中记录索引`i`的值。

因此，我们从控制台日志中记录了 0、1、2……一直到 9。

# 使用 Array.from 方法

我们也可以使用`Array.from`方法创建一个空数组，然后使用`Array.prototype.map`将空数组映射成我们想要的值数组。

例如，我们可以写:

```
const res = Array.from(Array(10)).map((_, i) => {
  return i * 10;
});
console.log(res)
```

然后我们得到和第一个例子一样的结果。

# 结论

我们可以重复运行代码`x`次，而不用用 JavaScript 数组方法和 spread 操作符创建一个带有可变索引变量的循环。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*