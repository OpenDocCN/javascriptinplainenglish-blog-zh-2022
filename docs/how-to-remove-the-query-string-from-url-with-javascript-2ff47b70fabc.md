# 如何用 JavaScript 删除 URL 中的查询字符串？

> 原文：<https://javascript.plainenglish.io/how-to-remove-the-query-string-from-url-with-javascript-2ff47b70fabc?source=collection_archive---------4----------------------->

![](img/05057d623796cfa99a7dc24041d29d2d.png)

Photo by [Aditya Wardhana](https://unsplash.com/@wardhanaaditya?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 删除 URL 的查询字符串部分。

在本文中，我们将看看如何用 JavaScript 删除 URL 字符串中的查询字符串部分。

# 使用 String.prototype.split 方法

我们可以使用 JavaScript string `split`方法从 URL 字符串中移除查询字符串。

例如，我们可以写:

```
const getPathFromUrl = (url) => {
  return url.split("?")[0];
}
const testURL = '/Products/List?SortDirection=dsc&Sort=price&Page=3&Page2=3&SortOrder=dsc'
console.log(getPathFromUrl(testURL))
```

创建返回查询字符串之前的 URL 部分的`getPathFromUrl`函数。

查询字符串总是跟在问号后面，所以我们可以对任何 URL 使用`split`。

我们调用`url`上的`split`，用`'?'`作为分隔符，用`[0]`获取查询字符串之前的部分。

因此，在控制台日志中，我们看到`'/Products/List’`被记录。

# 使用 String.prototype.replace 方法

从 URL 中删除查询字符串的另一种方法是使用 JavaScript string `replace`方法。

例如，我们可以写:

```
const getPathFromUrl = (url) => {
  return url.replace(/(\?.*)|(#.*)/g, "")
}
const testURL = '/Products/List?SortDirection=dsc&Sort=price&Page=3&Page2=3&SortOrder=dsc'
console.log(getPathFromUrl(testURL))
```

我们用正则表达式调用`replace`来删除在`?`之后的 URL 部分，以及在`#`符号之后的空字符串部分。

所以，我们得到了和上一个例子一样的结果。

# 结论

我们可以用一些字符串方法在 JavaScript 中去掉 URL 字符串的查询字符串部分。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和谐***](https://discord.gg/GtDtUAvyhW) ***。******