# 如何用 JavaScript 用正则表达式得到括号之间的字符串？

> 原文：<https://javascript.plainenglish.io/how-to-use-regular-expression-to-get-strings-between-parentheses-with-javascript-baf65ebf8d66?source=collection_archive---------5----------------------->

## 一个关于如何用 JavaScript 使用正则表达式得到括号之间的字符串的教程。

![](img/f7fa87eaa5109bbbab61957136093d72.png)

Photo by [Rahabi Khan](https://unsplash.com/@rahabikhan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在括号内的 JavaScript 字符串中获得子字符串。

在本文中，我们将看看如何使用 JavaScript 使用正则表达式来获取括号之间的字符串。

# 用 JavaScript 使用正则表达式获取括号内的字符串

我们可以使用`match`方法来获取字符串中匹配给定正则表达式模式的子字符串。

例如，我们可以写:

```
const txt = "I expect five hundred dollars ($500). and new brackets ($600)";
const regExp = /\(([^)]+)\)/g;
const matches = [...txt.match(regExp)];
console.log(matches)
```

我们创建`regExp`正则表达式来匹配括号中的任何内容。

`g`标志表示我们搜索所有匹配给定模式的子字符串。

然后我们用`regExp`调用`match`来返回一个在`txt`的括号之间的字符串数组。

所以，`matches`就是`[“($500)”, “($600)”]`。

我们也可以用以下方式排除带内括号的字符串:

```
/\(([^()]*)\)/g
```

使用`matchAll`方法，我们也可以获得括号内的子字符串，而不用括号。

为了使用它，我们写:

```
const txt = "I expect five hundred dollars ($500). and new brackets ($600)";
const regExp = /\(([^)]+)\)/g;
const matches = [...txt.matchAll(regExp)].flat();
console.log(matches)
```

我们调用`flat`来展平数组。

所以`matches`就是`[“($500)”, “$500”, “($600)”, “$600”]`。

# 结论

我们可以用 JavaScript 用正则表达式得到括号之间的字符串。

## 进一步阅读

[](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) [## 最佳网络抓取工具:beautiful soup vs . Regex vs . Advanced Web Scrapers

### BeautifulSoup、正则表达式或高级 web scraper——哪一个是 web 抓取的最佳工具？深潜…

javascript.plainenglish.io](/best-tool-for-web-scraping-beautifulsoup-vs-regex-vs-advanced-web-scrapers-50b8fb92950d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***