# 如何将 JavaScript 映射键转换成数组

> 原文：<https://javascript.plainenglish.io/how-to-convert-javascript-map-keys-to-an-array-a6de69318585?source=collection_archive---------5----------------------->

## 如何将 JavaScript 映射键转换成数组的指南。

![](img/f82f44eaf298fe3727b97643dfb6fe45.png)

Photo by [Tierra Mallorca](https://unsplash.com/@tierramallorca?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 映射让我们可以在代码中轻松存储键值对。

有时，我们可能希望将 JavaScript 映射键转换成一个数组。

在本文中，我们将研究如何将 JavaScript 映射键转换成数组。

# Array.from 方法和 Map.prototype.keys

我们可以用 map 的`keys`方法调用`Array.from`，将 map 的键转换成数组。

`keys`方法返回一个包含所有键的迭代器。

而`Array.from`方法将带键的迭代器转换成一个键数组。

例如，我们可以写:

```
const map = new Map()
  .set('a', 1)
  .set('b', 2);
const keys = Array.from(map.keys());
console.log(keys)
```

我们创建一个新的`Map`实例来创建地图。

然后我们调用`set`，按照这个顺序传递我们想要设置的键和值。

接下来，我们调用返回值为`map.keys`的`Array.from`，将带有映射键的迭代器返回到一个数组。

因此我们得到:

```
["a", "b"]
```

作为`keys`的值。

# 展开运算符和 Map.prototype.keys

同样，我们可以将 spread 操作符与`keys`方法一起使用，将带有键的迭代器转换成一个键数组。

例如，我们可以写:

```
const map = new Map()
  .set('a', 1)
  .set('b', 2);
const keys = [...map.keys()];
console.log(keys)
```

对于`keys`，我们得到了相同的结果。

# 结论

我们可以用`Map.prototype.keys`方法返回一个带有映射键的迭代器。

然后我们可以用`Array.from`方法或 spread 操作符将带键的迭代器转换成一个键数组。

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***