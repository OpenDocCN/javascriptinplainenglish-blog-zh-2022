# 如何将一个 Javascript 对象编码成查询字符串？

> 原文：<https://javascript.plainenglish.io/how-to-encode-a-javascript-object-into-a-query-string-ab56554107cb?source=collection_archive---------11----------------------->

![](img/d4e899b20415cfbaf0a3561fb19233d1.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们不得不将 JavaScript 对象的数据转换成查询字符串，我们可以用它来发出 HTTP 请求。

在本文中，我们将研究如何将 JavaScript 对象编码成查询字符串。

# `URLSearchParams Constructor`

我们可以使用`URLSearchParams`构造函数轻松地从 JavaScript 对象创建查询字符串。

它适用于当前大多数浏览器。

例如，我们可以写:

```
const object = {
  a: 1,
  b: 2,
  c: undefined,
  d: null
}
const queryString = new URLSearchParams(object).toString()
console.log(queryString)
```

我们将想要转换成查询字符串的`object`直接传入`URLSearchParams`构造函数。

然后我们调用`toString`来返回查询字符串。

所以`queryString`是:

```
'a=1&b=2&c=undefined&d=null'
```

`undefined`和`null`都转换成字符串。

属性名用作键，属性值用作值。

我们还可以遍历对象，用`append`方法插入查询参数:

```
const object = {
  a: 1,
  b: 2,
  c: undefined,
  d: null
}
const searchParams = new URLSearchParams()
Object.keys(object).forEach(key => {
  searchParams.append(key, object[key])
});
const queryString = searchParams.toString()
console.log(queryString)
```

我们调用`Object.keys`来获取`object`中的密钥。

然后我们用`key`调用`forEach`从`object`获取密钥。

然后调用`append`分别添加键和值作为参数。

然后我们调用`searchParams.toString`来返回查询字符串。

因此，对于`queryString`，我们得到与之前相同的结果。

我们可以简单地用`Object.entries`方法调用`forEach`来获得一个键值对的数组。

所以我们写道:

```
const object = {
  a: 1,
  b: 2,
  c: undefined,
  d: null
}
const searchParams = new URLSearchParams()
Object.entries(object).forEach(([key, value]) => {
  searchParams.append(key, value)
});
const queryString = searchParams.toString()
console.log(queryString)
```

创建查询字符串。

在`forEach`回调中，我们用参数构造的`key`和`value`调用`append`来插入查询参数。

所以我们得到了和以前一样的结果。

# 结论

我们可以用大多数浏览器都有的`URLSeacrhParams`构造函数将 JavaScript 对象编码成查询字符串。

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*