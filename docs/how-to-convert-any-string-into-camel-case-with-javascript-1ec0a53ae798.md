# 如何用 JavaScript 将任意字符串转换成 Camel Case？

> 原文：<https://javascript.plainenglish.io/how-to-convert-any-string-into-camel-case-with-javascript-1ec0a53ae798?source=collection_archive---------0----------------------->

## 用 JavaScript 将任意字符串转换成骆驼大小写的教程。

![](img/1bf47b646f9da3b0da30e1657398b96b.png)

Photo by [Wolfgang Hasselmann](https://unsplash.com/@wolfgang_hasselmann?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 把一个 JavaScript 字符串转换成 camel case。

在本文中，我们将看看如何用 JavaScript 将任何字符串转换成 camel case。

# 使用 String.prototype.replace 方法

我们可以使用 string instances 的'`replace`方法来转换字符串中的每个单词，将第一个单词转换成小写，其余的单词转换成大写，然后去掉空格。

为此，我们写道:

```
const camelize = (str) => {
  return str.replace(/(?:^\w|[A-Z]|\b\w)/g, (word, index) => {
    return index === 0 ? word.toLowerCase() : word.toUpperCase();
  }).replace(/\s+/g, '');
}console.log(camelize("EquipmentClass name"));
```

我们用一个正则表达式调用`replace`，这个正则表达式用`\b`和`\w`寻找单词边界。

`\b`匹配一个退格键。

`\w`匹配拉丁字母中的任何字母数字字符。

我们检查`index`来确定它是否是第一个单词。

如果它是 0，那么我们返回`word.toLowerCase()`将它从单词的第一个字符转换成小写，因为它是第一个单词。

否则，我们返回`word.toUpperCase`将单词的第一个字符转换成大写。

然后我们用`/\s+/g`和一个空字符串再次调用`replace`，用空字符串替换空格。

因此，`camelize`返回结果`'equipmentClassName’`。

# 洛达什驼峰法

我们可以使用 Lodash `camelCase`方法将任何字符串转换成 camel case，方式与`camelize`函数相同。

例如，我们可以写:

```
console.log(_.camelCase("EquipmentClass name"));
```

然后我们得到和上一个例子一样的结果。

# 结论

我们可以用`String.prototype.replace`方法或 Lodash `camelCase`方法将任何 JavaScript 字符串转换成 camel case。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*