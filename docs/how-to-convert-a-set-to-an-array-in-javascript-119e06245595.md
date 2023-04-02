# 如何在 JavaScript 中将集合转换成数组？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-set-to-an-array-in-javascript-119e06245595?source=collection_archive---------7----------------------->

![](img/32c6df80b89e0307535ddc524095fec6.png)

Photo by [Sander Weeteling](https://unsplash.com/@sanderweeteling?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们使用集合来创建一个没有重复元素的数据结构。

但是我们必须把它们转换成一个数组，这样我们才能更容易地使用它们。

在本文中，我们将研究将 JavaScript 集合转换成 JavaScript 数组的方法。

# 数组. from

静态方法让我们将任何可迭代的对象转换成一个数组。

JavaScript 集合是可迭代的对象，所以我们可以用它们来进行转换。

例如，我们可以写:

```
const array = Array.from(new Set([1, 2, 3]));
console.log(array)
```

将集合转换为数组。

我们将集合直接传递给`Array.from`方法来进行转换。

因此，`array`是:

```
[1, 2, 3]
```

# 传播算子

将集合转换为数组的另一种方法是使用 spread 运算符。

spread 操作符允许我们将任何可迭代对象扩展到一个数组中。

因此，我们可以这样写:

```
const array = [...new Set([1, 2, 3])];
console.log(array)
```

因此，我们得到和以前一样的结果。

# Set.prototype.forEach

JavaScript 集合有一个`forEach`方法，让我们可以遍历集合中的所有条目。

它接受一个回调函数，这个回调函数将我们正在迭代的项作为参数，我们可以在函数体中对它做任何事情。

例如，我们可以写:

```
const set = new Set([1, 2, 3])
const array = [];
set.forEach(v => array.push(v));
console.log(array)
```

得到和以前一样的结果。

我们调用`array.push`将集合项`v`追加到`array`中。

# Set.prototype.values 和扩展运算符

JavaScript 集合也有一个`values`方法，该方法返回一个迭代器，其中包含集合的所有值。

所以我们可以用 spread 操作符将迭代器扩展到一个数组中。

例如，我们可以写:

```
const set = new Set([1, 2, 3])
const array = [...set.values()]
console.log(array)
```

将迭代器中由`set.values`返回的值分散到`array`中。

所以我们得到了和以前一样的结果。

# for-of 循环

由于 JavaScript 集是可迭代的，我们可以用 for-of 循环遍历条目。

并且在循环体中，我们可以调用`push`将设置项追加到数组中。

为此，我们写道:

```
const set = new Set([1, 2, 3])
const array = [];
for (const v of set) {
  array.push(v)
}
console.log(array)
```

我们得到了和以前一样的结果。

# 结论

有很多方法可以将集合转换成数组。

由于 JavaScript 集合是可迭代的对象，我们可以使用 spread 操作符、for-of 循环、`Array.from`等。进行转换。

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*