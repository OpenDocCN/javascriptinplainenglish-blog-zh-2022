# 如何返回 JavaScript 数组中最大值的索引？

> 原文：<https://javascript.plainenglish.io/how-to-return-the-index-of-the-greatest-value-in-a-javascript-array-4143b54a06?source=collection_archive---------3----------------------->

## 关于如何返回 JavaScript 数组中较大值的索引的教程。

![](img/6c3a6880556b98a98bef3c0bdefa6bf3.png)

Photo by [Sangga Rima Roman Selia](https://unsplash.com/@sxy_selia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望返回 JavaScript 数组中最大值的索引。

在本文中，我们将研究如何返回 JavaScript 数组中较大值的索引。

# 使用 Array.prototype.indexOf 和 Math.max 方法

我们可以用`Math.max`和数组的`indexOf`方法找到 JavaScript 数组中最大值的索引。

例如，我们可以写:

```
const arr = [0, 21, 22, 7];
const index = arr.indexOf(Math.max(...arr));
console.log(index)
```

我们通过将`arr`扩展到`Math.max`方法中来调用带有`arr`元素的`Math.max`。

这将返回`arr`中最大的元素。

然后我们可以在`arr`的最大元素上调用`arr.indexOf`。

所以`index`是 2，这是`arr`中值 22 的索引。

# 使用 Array.prototype.reduce 方法

获取数组中最大元素的索引的另一种方法是使用 JavaScript 数组的`reduce`方法。

为了使用它，我们写:

```
const arr = [0, 21, 22, 7];
const index = arr.reduce((iMax, x, i, arr) => x > arr[iMax] ? i : iMax, 0);
console.log(index)
```

我们用一个带有`iMax`参数的回调来调用`arr`上的`reduce`，这个参数是目前为止`arr`的最大值的索引。

`x`是正在被迭代的`arr`的条目。

`i`是`x`的索引。

`arr`是`arr`阵本身。

我们通过检查`x`是否大于被记录为最大 so 条的当前元素(即`arr[iMax]`)来返回最大元素的索引。

如果`x`大于`arr[iMax]`，我们返回`i`。

否则，我们返回`iMax`。

0 是`arr`最大元素索引的初始值。

因此`index`是 2，正如我们在前面的例子中看到的。

# 结论

我们可以使用`Math.max`和`Array.prototype.indexOf`或`Array.prototype.reduce`方法来获取 JavaScript 数组中最大元素的索引。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *。**