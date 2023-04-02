# 如何用 JavaScript 修剪字符串中的特定字符

> 原文：<https://javascript.plainenglish.io/how-to-trim-a-specific-character-from-a-string-with-javascript-1dd7f9e9c37f?source=collection_archive---------6----------------------->

## 关于如何用 JavaScript 从字符串中删除特定字符的教程。

![](img/6bf2fd3ec61cfea286b75f13a8bb38b5.png)

Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 从字符串中删除一个特定的字符。

在本文中，我们将看看如何用 JavaScript 从字符串中删除特定的字符。

# 使用 String.prototype.replace 方法

我们可以使用 JavaScript 字符串的`replace`方法删除给定字符的所有实例。

为了使用它，我们写:

```
const x = '|f|oo||';
const y = x.replace(/^\|+|\|+$/g, '');
console.log(y);
```

我们有了想要从中移除`||`子字符串的字符串`x`，

然后我们调用与`x`中的`||`子串匹配的正则表达式来替换它们。

`g`标志匹配给定模式的所有实例。

我们传递给`replace`的第二个参数是一个空字符串，所以我们删除了与第一个参数中的模式匹配的子字符串的所有实例。

所以，`y`就是`'f|oo’`。

# 使用 String.prototype.replaceAll 方法

我们可以用 ES2021 附带的 JavaScript string `replaceAll`方法做同样的事情。

例如，我们可以写:

```
const x = '|f|oo||';
const y = x.replaceAll(/^\|+|\|+$/g, '');
console.log(y);
```

用`replaceAll`替换`replace`。

我们传入的正则表达式必须有`g`标志，否则我们会得到一个错误，因为它只能替换所有匹配给定模式的子字符串。

所以我们得到了和上一个例子一样的结果。

# 结论

我们可以使用 JavaScript string `replace`或`replaceAll`方法删除所有匹配给定模式的子字符串。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***