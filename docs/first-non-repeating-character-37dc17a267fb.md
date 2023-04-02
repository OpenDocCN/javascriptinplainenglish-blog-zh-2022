# 用 JavaScript 查找字符串中第一个不重复的字符

> 原文：<https://javascript.plainenglish.io/first-non-repeating-character-37dc17a267fb?source=collection_archive---------9----------------------->

## 如何用 JavaScript 找到字符串中第一个不重复的字符

![](img/4ec4b4120a0a9b90f295eef95701ae13.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这就是…最后的*简单算法专家问题！*

我非常兴奋能够进入中级领域，在那里事情肯定会变得更加令人兴奋

你们中的许多人可能对这个问题很熟悉。

我们将得到一个输入字符串，我们的任务是返回第一个唯一值(一个不重复的值)的索引。如果我们找不到这样的值，我们将返回-1。

***我的做法:***

我将遍历输入字符串，查看当前值之前的所有值*和当前值*之后的所有值*，检查是否重复。如果没有找到，我就返回当前索引。*

另一方面，如果我已经遍历了整个数组，但从未满足这些条件，我将返回-1。

# 密码！

这就是了。

我在第 3 行和第 4 行中的“before”和“after”只是组成数组其余部分的快照。

使用这些我可以确定我的当前值是否是不重复的。

完成和*完成…*

希望我会在 AlgoExpert 中等难度问题中见到你！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***