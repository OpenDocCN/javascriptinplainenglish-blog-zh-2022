# 为什么不用这么强大的正则表达式呢？

> 原文：<https://javascript.plainenglish.io/why-dont-you-use-such-powerful-regular-expressions-8aa33732a951?source=collection_archive---------5----------------------->

## 每个开发人员都应该知道的 15 个正则表达式技巧

![](img/fecf8f1ff32fcd196f6bc9975268e765.png)

Photo by [Steve Tsang](https://unsplash.com/@stevetsang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你对正则表达式有什么看法？我猜你会说**太晦涩**，**我对它一点兴趣都没有**。是的，我曾经和你一样，以为这辈子都学不会。

但是我们不能否认它真的很强大，我在工作中用的很多，并且**我总结了 15 个小技巧和大家分享。**

如果你对它们是如何实现的感兴趣，非常欢迎你在评论区告诉我，我会另写一篇文章单独分析。

# 1.格式化货币

我经常需要格式化货币，它需要遵循以下规则:

1.  `123456789` = > `123,456,789`
2.  `123456789.123` = > `123,456,789.123`

![](img/872e63cce0bad4016202fc33a8e94f17.png)

你能想象如果没有正则表达式我们会怎么做吗？

# 2.实现微调功能的两种方法

有时我们需要删除字符串的前导和尾随空格，使用正则表达式会非常方便，我想和你分享至少两种方法。

**方式 1**

很好，我们已经删除了字符串“string”的前导空格和尾随空格。

![](img/9016dc877e1bcc8a660b5a9df04de93c.png)

**方式二**

第二种方式，我们也达到了目的。

![](img/83d0e9af8514350b3d5b7e75a16198ac.png)

# 3.解析链接上的搜索参数

您一定也经常需要从链接中获取参数，对吗？

用正则表达式解决这个问题真的很简单。

![](img/1ce0f695902cd4337555beaf746cb13f.png)

# 4.骆驼盒绳子

请将字符串转换为骆驼大小写，如下所示:

我的朋友们，没有什么比正则表达式更好的了。

![](img/728046ebaedb09ae7b11f51a6cbdc32f.png)

# 5.将字符串的第一个字母转换为大写

请将`hello world`转换为`Hello World`。

![](img/d21ecce9d036f1f13e0e0c9be6fd485c.png)

# 6.转义 HTML

防止 XSS 攻击的方法之一是进行 HTML 转义。转义规则如下:

![](img/a9d302c88a687049361ae3de18c977e5.png)![](img/6238c9b409c216e32364c638891a770d.png)

# 8.Unescape HTML

![](img/821a74b5370eba98ce0312a4798f1188.png)

# 9.24 小时格式的匹配时间

请判断时间是否符合 24 小时格式。匹配规则如下:

1.  01:14
2.  1:14
3.  1:1
4.  23:59

![](img/3f865a9e1e0f30e13f6ddd13a38adec1.png)

# 10.匹配日期格式

请匹配类似(yyyy-mm-dd，yyyy.mm.dd，yyyy/mm/dd)的日期格式，例如 2021–08–22，2021.08.22，2021/08/22。

![](img/03395e02270cfaab77355e0fc590d3e2.png)

# 11.以十六进制匹配颜色值

请从字符串中获取十六进制颜色值。

![](img/c5c7728ae9a1cfd1d49cbe57e608dc9f.png)

# 12.检查 URL 的前缀是 HTTPS 还是 HTTP

# 13.请检查版本号是否正确

版本号必须采用 x.y.z 格式，其中 XYZ 至少是一位数字。

![](img/cfcc17691024b6e737d4b402080ca9c0.png)

# 14.获取网页上所有 img 标签的图片地址

![](img/e088ce89c9d693628a48bd42bbf2387e.png)

# 15.根据 3–4–4 格式划分电话号码

![](img/b582367b8e3cdeef6ae8376099cc716a.png)

# 最后

**感谢阅读。**我期待着期待您的关注和阅读更多高质量的文章。

[](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [## 记者:在 JavaScript 中(a==1 && a==2 && a==3)能计算为真吗？

### 是的，这可能是真的，而且有 6 种方式——太神奇了！

javascript.plainenglish.io](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [## “我失去了一个工作机会，只是因为承诺。所有”

### 一次让我好难过的面试经历。

javascript.plainenglish.io](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***