# 如何在 JavaScript 中去掉一个“:”前的部分字符串？

> 原文：<https://javascript.plainenglish.io/how-to-remove-part-of-a-string-before-a-in-javascript-f8f2420323c9?source=collection_archive---------10----------------------->

![](img/c6741b67553c98d4595e06de6df9ea82.png)

Photo by [MAYANK D](https://unsplash.com/@mayank_dimri?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 删除冒号前的 JavaScript 字符串的一部分。

在本文中，我们将看看如何用 JavaScript 删除冒号前的 JavaScript 字符串部分。

# 使用 String.prototype.substring 方法

删除冒号前的部分字符串的一种方法是使用 JavaScript 字符串的`substring`方法。

例如，我们可以写:

```
const str = "Abc: Lorem ipsum sit amet";
const newStr = str.substring(str.indexOf(":") + 1);
console.log(newStr)
```

我们使用`indexOf`方法来获取第一个冒号的索引。

然后我们在传递给`substring`的值上加 1，得到第一个冒号后的子串。

因此，`newStr`就是`'Lorem ipsum sit amet’`。

# 使用 Array.prototype.split 和 Array.prototype.pop 方法

另一种删除冒号前字符串的方法是使用 JavaScript 数组的`split`和`pop`方法。

为此，我们写道:

```
const str = "Abc: Lorem ipsum sit amet";
const newStr =  str.split(":").pop();
console.log(newStr)
```

我们调用`str`上的`split`来使用冒号作为分隔符将`str`分割成一个数组。

然后我们调用`pop`返回`split`返回的数组的最后一个元素。

所以我们得到了和以前一样的结果。

# 使用正则表达式

我们还可以使用正则表达式按照给定的分隔符分割字符串，并从分割的字符串中获得我们想要的部分。

例如，我们可以写:

```
const str = "Abc: Lorem ipsum sit amet";
const newStr = /:(.+)/.exec(str)[1];
console.log(newStr)
```

在匹配冒号分隔符的正则表达式上调用`exec`。

我们使用索引 1 从拆分字符串中获取第二项。

所以我们得到了和以前一样的结果。

# 结论

删除冒号前的部分字符串的一种方法是使用 JavaScript 字符串的`substring`方法。

另一种删除冒号前字符串的方法是使用 JavaScript 数组的`split`和`pop`方法。

我们还可以使用正则表达式按照给定的分隔符分割字符串，并从分割的字符串中获得我们想要的部分。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们关于 [**推特**](https://twitter.com/inPlainEngHQ)[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**[**不和**](https://discord.gg/GtDtUAvyhW) **。******

## ****想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。****

****我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。****