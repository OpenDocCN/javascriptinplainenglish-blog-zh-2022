# 如何在 JavaScript 中使用 Regex 去掉一个字符串中的所有标点符号？

> 原文：<https://javascript.plainenglish.io/how-to-strip-all-punctuation-from-a-string-in-javascript-using-regex-99c6857790d1?source=collection_archive---------2----------------------->

![](img/73b54374f196b7b77440bc1b1691ede4.png)

Photo by [Jixiao Huang](https://unsplash.com/@fatbird2333?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用正则表达式去掉 JavaScript 字符串中的所有标点符号。

在本文中，我们将研究如何用 regex 去除 JavaScript 字符串中的所有标点符号。

# 使用 String.prototype.replace 方法

我们可以使用 JavaScript string `replace`方法获得匹配正则表达式模式的字符串的所有部分，并用我们想要的替换它们。

例如，我们可以写:

```
const s = "This., -/ is #! an $ % ^ & * example ;: {} of a = -_ string with `~)() punctuation";
const punctuationless = s
  .replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g, "")
  .replace(/\s{2,}/g, " ");
console.log(punctuationless)
```

我们有一个`s`字符串，其中有许多我们想要删除的标点符号。

接下来，我们第一次用正则表达式调用`replace`，这个正则表达式包含了我们想要删除的所有标点符号。

`g`标志表示我们匹配字符串中与给定模式匹配的所有实例。

我们用一个空字符串替换它们，就像我们用第二个参数表示的那样。

然后我们用一个匹配 2 个或更多空格的正则表达式再次调用`replace`。

我们用一个空格替换那些空格。

所以`punctuationless`应该是`‘This is an example of a string with punctuation’`。

# 结论

我们可以使用 JavaScript string `replace`方法和正则表达式来匹配我们想要替换的字符串中的模式。

因此，我们可以使用它来删除标点符号，方法是匹配标点符号并用空字符串替换它们。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***