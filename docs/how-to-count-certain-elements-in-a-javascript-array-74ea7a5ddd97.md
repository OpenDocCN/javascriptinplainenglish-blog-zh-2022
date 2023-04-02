# 如何计算一个 JavaScript 数组中的某些元素？

> 原文：<https://javascript.plainenglish.io/how-to-count-certain-elements-in-a-javascript-array-74ea7a5ddd97?source=collection_archive---------11----------------------->

![](img/43f555e78059db016336ee9054d72745.png)

Photo by [Raychan](https://unsplash.com/@wx1993?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要计算 JavaScript 数组中的某些元素。

在本文中，我们将了解如何计算 JavaScript 数组中的某些元素。

# 使用 Array.prototype.filter 方法

`Array.prototype.filter`方法让我们返回一个包含满足我们所寻找的条件的条目的数组。

所以我们可以利用`filter`返回的数组的`length`属性来统计满足给定条件的元素。

例如，我们可以写:

```
const arr = [1, 2, 3, 5, 2, 8, 9, 2]
const numEvens = arr.filter(x => x % 2 === 0).length
console.log(numEvens)
```

我们有带一些数字的`arr`。

为了计数数组中所有的偶数，我们可以使用带有返回`x % 2 === 0`的回调的`filter`方法来返回一个满足这个条件的数组，这些数组都是偶数。

然后我们可以使用`length`属性来获取数组中条目的数量。

所以我们从控制台日志中看到`numEvens`等于 4。

# 使用 Array.prototype.reduce 方法

同样，我们可以使用`Array.prototype.reduce`方法来计算满足给定条件的项目数。

为了用`reduce`计算偶数的个数，我们写:

```
const arr = [1, 2, 3, 5, 2, 8, 9, 2]
const numEvens = arr.reduce((total, x) => (x % 2 === 0 ? total + 1 : total), 0)
console.log(numEvens)
```

我们用带有`total`和`x`参数的回调来调用`reduce`。

`total`是目前返回的总数，`x`是被迭代以计算`total`的值。

如果`x % 2`为 0，我们返回`total + 1`，否则返回`total`。

第二个参数中的`0`是`total`的初始值。

因此，我们应该得到和以前一样的`numEvens`的值。

# 结论

我们可以用数组实例`filter`或`reduce`方法对数组中的某些元素进行计数。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*