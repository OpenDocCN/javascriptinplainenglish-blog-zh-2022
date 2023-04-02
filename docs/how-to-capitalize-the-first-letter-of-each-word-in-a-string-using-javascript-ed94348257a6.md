# 如何使用 JavaScript 将字符串中每个单词的首字母大写

> 原文：<https://javascript.plainenglish.io/how-to-capitalize-the-first-letter-of-each-word-in-a-string-using-javascript-ed94348257a6?source=collection_archive---------5----------------------->

![](img/5ecf4131fc42b88f26987bb35c604582.png)

Photo by [katalin gyurasics](https://unsplash.com/@gyurasics?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望使用 JavaScript 将字符串中每个单词的第一个字母大写。

在本文中，我们将看看如何用 JavaScript 将字符串中每个单词的首字母大写。

# 使用 String.prototype.toUpperCase 和 String.prototype.substring 方法

我们可以使用 string `toUpperCase`和`substring`方法将字符串中的每个单词的首字母转换为大写。

例如，我们可以写:

```
const titleCase = (str) => {
  const splitStr = str.toLowerCase().split(' ');
  for (const [i, str] of splitStr.entries()) {
    splitStr[i] = str[0].toUpperCase() + str.substring(1);
  }
  return splitStr.join(' ');
}console.log(titleCase("I'm a little tea pot"));
```

我们用`str`字符串参数创建了`titleCase`函数。

我们用`split`方法按空格字符分割字符串。

然后我们用 for-of 循环遍历拆分字符串数组中的每个字符串。

我们通过析构由`entries`返回的条目，从每个条目中获得索引`i`和字符串`str`。

之后，我们获取`str`的第一个字符，并将其转换为大写。然后，我们将它与从`substring`获得的`str`字符串的其余部分连接起来。

最后，我们使用`join`在每个单词之间添加一个空格，将字符串连接起来。

因此，控制台日志应该记录`'I’m A Little Tea Pot’`。

# 结论

我们可以通过将字符串拆分成单词，转换标题中的每个单词，然后将单词连接在一起，从而将字符串转换成标题大小写。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***