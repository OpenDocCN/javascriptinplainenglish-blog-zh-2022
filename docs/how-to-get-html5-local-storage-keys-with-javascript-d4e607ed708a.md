# 如何用 JavaScript 获取 HTML5 本地存储密钥？

> 原文：<https://javascript.plainenglish.io/how-to-get-html5-local-storage-keys-with-javascript-d4e607ed708a?source=collection_archive---------1----------------------->

## 关于如何用 JavaScript 获取存储在本地存储中的项目的键的指南。

![](img/606ce9f91c115186e9ed320724ff51dc.png)

Photo by [Mariah Solomon](https://unsplash.com/@heymemento?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望获得存储在浏览器本地存储中的项目的密钥。

在本文中，我们将研究如何用 JavaScript 获取存储在本地存储中的条目的键。

# 使用 Object.entries 方法

我们可以使用`Object.entries`方法来获取存储在本地存储中的项的键和值。

例如，我们可以写:

```
localStorage.setItem('foo', 1)
localStorage.setItem('bar', 2)
const entries = Object.entries(localStorage)
console.log(entries)
```

那么`entries`就是:

```
[
  [
    "foo",
    "1"
  ],
  [
    "bar",
    "2"
  ]
]
```

因为`Object.entries`在`localStorage`对象中返回一个键值对数组。

我们将`localStorage.setItem`与项的键和值一起使用，我们希望将它们分别存储为参数。

# 使用 Object.keys 方法

此外，我们可以使用`Object.keys`方法来获取存储在本地存储中的条目的键。

例如，我们可以写:

```
localStorage.setItem('foo', 1)
localStorage.setItem('bar', 2)
const keys = Object.keys(localStorage)
console.log(keys)
```

那么`keys`就是`[“foo”, “bar”]`。

# 使用 localStorage.key 方法

另一种获取存储在本地存储器中的项目的所有键的方法是使用`localStorage.key`方法。

我们可以使用它和`localStorage.length`属性创建一个数组来填充键。

`localStorage.length`已经存储在本地存储器中的项目数。

要使用它们，我们可以写:

```
localStorage.setItem('foo', 1)
localStorage.setItem('bar', 2)
const keys = [...Array(localStorage.length)].map((o, i) => {
  return localStorage.key(i);
})
console.log(keys)
```

我们扩展长度为`localStorage.length`的空数组，将其扩展到一个新数组中，然后用回调函数调用`map`来返回我们通过调用索引为`i`的`localStorage.key`得到的键。

结果，`keys`也是`[“foo”, “bar”]`。

# 结论

通过 JavaScript，我们可以使用几种方法来获取存储在本地存储中的项目。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*