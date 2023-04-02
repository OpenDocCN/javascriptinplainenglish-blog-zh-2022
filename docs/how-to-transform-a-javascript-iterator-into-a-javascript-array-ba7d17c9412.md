# 如何将一个 JavaScript 迭代器转换成 JavaScript 数组？

> 原文：<https://javascript.plainenglish.io/how-to-transform-a-javascript-iterator-into-a-javascript-array-ba7d17c9412?source=collection_archive---------13----------------------->

![](img/da52a942a0f1920a332d108ff4d53b4d.png)

Photo by [Sandy Millar](https://unsplash.com/@sandym10?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们在 JavaScript 代码中有一个迭代器对象，我们想把它转换成一个数组。

在本文中，我们将研究如何将 JavaScript 迭代器转换成 JavaScript 数组。

# 使用 Array.from 方法

将 JavaScript 迭代器转换成 JavaScript 数组的一种方法是使用`Array.from`静态方法。

例如，我们可以写:

```
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3],
])
const arr = Array.from(map.entries());
console.log(arr)
```

我们创建了一个`Map`实例，该实例具有返回迭代器的`entries`方法，该迭代器从映射中返回键值对。

然后我们将从`entries`方法返回的迭代器传递给`Array.from`方法，从迭代器返回一个键值对数组。

因此，`arr`的值为:

```
[
  [
    "a",
    1
  ],
  [
    "b",
    2
  ],
  [
    "c",
    3
  ]
]
```

# 使用扩展运算符

我们可以用 spread 操作符做与`Array.from`方法相同的事情。

它还允许我们将迭代器对象转换为数组。

例如，我们可以写:

```
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3],
])
const arr = [...map.entries()];
console.log(arr)
```

将`map.entries`返回的迭代器分散到一个数组中。

键值对数组被分散到`arr`数组中。

因此，`arr`又是一次:

```
[
  [
    "a",
    1
  ],
  [
    "b",
    2
  ],
  [
    "c",
    3
  ]
]
```

这与前面的例子相同。

# 结论

我们可以使用`Array.from`方法或 spread 操作符轻松地将 JavaScript 迭代器对象转换成 JavaScript 数组。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***