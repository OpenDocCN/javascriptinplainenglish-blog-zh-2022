# JavaScript URL 对象入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-the-javascript-url-object-e5de2ea67a92?source=collection_archive---------3----------------------->

## JAVASCRIPT 教程

## 了解如何在 JavaScript 中正确处理 URL

![](img/e84fda42e2be7f863e900f4511502e85.png)

如果你已经做了一段时间的开发人员，毫无疑问你以前也使用过 URL。既有趣又令人沮丧的是，像 URL 操作这样简单的事情怎么会变得如此混乱和容易出错。

在本文中，我想深入探讨 JavaScript URL 对象。这个对象消除了处理 URL 的大部分麻烦，帮助我们编写更干净、更好的代码。

## 创建 URL 对象

使用 URL 构造函数方法创建一个 URL 对象。您可以将完整的 url 传递给构造函数，也可以将可选的基 URL 作为第二个参数来传递路径。

您可以通过它的公共属性进一步构造 URL。

注意，URL 是根据 [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986) 中的规则编码的。例如:

## 从 URL 读取信息

您可以使用相同的属性从 URL 中检索信息。

## 用例

让我们创建一个简单的方法，它基于一个基本 URL 和一个查询参数数组来构造一个 URL。我们将通过两种方式做到这一点，首先是传统的方式，其次是使用 URL 对象。

除了第二个函数可读性更好之外，第二种方法还有几个好处。

*   我们不必考虑`‘?’`和`‘&’`字符。
*   我们不必手动构建字符串。
*   **参数是自动编码的**，就是有人在参数中注入一个空格或特殊字符，代码不会被破解。

## 额外资源

*   [MDN 文档:URL 对象](https://developer.mozilla.org/en-US/docs/Web/API/URL)

## 结论

URL 对象是一个非常有用的附加功能，它使得处理 URL 不容易出错，同时也更容易。

感谢阅读。如果你对此有想法，一定要留下评论！

如果你喜欢我的内容，并想支持我的努力，考虑通过[我的会员链接](https://medium.com/@WesleySmits/membership)成为一个媒体订阅者。这不会花费你任何额外的费用，但 Medium 会把部分收益给我，让我推荐你。

如果你愿意，你可以在 [LinkedIn](https://www.linkedin.com/in/wesley-robert-smits/) 或 [Twitter](https://twitter.com/iamwesleysmits) 上联系我！

[](https://medium.com/@WesleySmits/membership) [## 通过我的推荐链接加入 Medium-Wesley Smits

### 阅读韦斯利·斯密特(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

medium.com](https://medium.com/@WesleySmits/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***