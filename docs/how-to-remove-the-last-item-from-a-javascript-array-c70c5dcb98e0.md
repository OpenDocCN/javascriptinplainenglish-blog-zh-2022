# 如何从 JavaScript 数组中移除最后一项？

> 原文：<https://javascript.plainenglish.io/how-to-remove-the-last-item-from-a-javascript-array-c70c5dcb98e0?source=collection_archive---------2----------------------->

![](img/58fea79c1296cef01ccecdc92d27c9c2.png)

Photo by [Mihály Köles](https://unsplash.com/@mihaly_koles?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 JavaScript 数组中删除最后一项是我们有时不得不对代码做的事情。

在本文中，我们将研究如何从 JavaScript 数组中移除最后一项。

# 数组.原型.拼接

我们可以使用 JavaScript 数组的`splice`方法从数组中移除最后一项。

例如，我们可以写:

```
const array = [1, 2, 3]
array.splice(-1, 1)
console.log(array)
```

我们用-1 调用`splice`来删除数组中的最后一项。

而 1 指定移除一个项目。

那么`array`就是`[1, 2]`。

# 数组.原型. pop

我们可以调用`pop`方法从数组中移除最后一项。

它返回被删除的项目。

要使用它，我们可以写:

```
const array = [1, 2, 3]
const popped = array.pop()
console.log(popped, array)
```

我们调用`array`上的`pop`来移除`array`中的最后一项。

并且我们将移除的项目分配给`popped`。

所以`popped`是 3。

而`array`就是`[1, 2]`。

# 数组.原型.切片

我们可以用来从数组中移除最后一项的另一个数组方法是`slice`方法。

它返回一个带有开始和结束索引的数组。

例如，我们可以写:

```
const array = [1, 2, 3]
const newArr = array.slice(0, -1);
console.log(newArr)
```

我们用起始和结束索引调用`slice`来返回一个从起始索引到结束索引的数组。

不包括结束索引处的项目，但包括开始索引处的项目。

数字-1 表示数组中最后一项的索引。

因此，我们得到:

```
[1, 2]
```

作为`newArr`的值。

# 数组.原型.过滤器

我们可以使用 array `filter`方法返回一个包含满足给定条件的项目的数组。

因此，我们可以检查该项是否在数组的最后一个索引中。

例如，我们可以写:

```
const array = [1, 2, 3]
const newArr = array.filter((element, index) => index < array.length - 1);
console.log(newArr)
```

我们向返回`index < array.length — 1`的`filter`方法传递一个回调，以返回索引小于`array.length — 1`的所有项目。

因此，我们将为`newArr`获得与上一个示例相同的结果。

# 结论

我们可以使用 JavaScript 数组方法从数组中移除最后一项。

*更多内容看* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*