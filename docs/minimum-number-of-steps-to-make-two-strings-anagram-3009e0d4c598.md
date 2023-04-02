# 组成两个字符串的变位词的最少步骤数

> 原文：<https://javascript.plainenglish.io/minimum-number-of-steps-to-make-two-strings-anagram-3009e0d4c598?source=collection_archive---------14----------------------->

## LeetCode #1347

啊…在技术面试中失败的挫败感。

最糟糕的是，我几乎在开始的 15 分钟内就解决了问题，但却做出了一个荒谬的决定，用“新方法”重新开始。

吸取教训。

[问题](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)是这样的:

我们得到两个字符串，保证长度相等，然后返回使它们成为变位词所需的最小变化量(每个字母的数量相同，但排列不同)。

在未能通过计时黑客等级评估的所有测试后，我又花了 5 分钟在 Leetcode 上，并使其工作。

让我们开始吧

***想通了……***

为了比较每个字符串中的字符，我需要计数每个单词中的所有字符。

在这一点上，我需要有意义地比较这些值，以给出使计数匹配所需的最小变化量。

这就是我第一次尝试失败的原因——我决定关注字符数之间的*差异*并返回该值。

然而，在我成功的后续研究中，首先关注这两个字母有什么共同点，然后从字符串长度中减去达到变位词状态所需的变化次数，似乎容易得多。

***编码出来……***

这非常简单，为了清楚起见，我还添加了一些注释。

可能从一些解释中受益的一行是#29。

当一个字符同时出现在两个单词中但出现频率不同时,“minMatch”赋值有助于量化匹配度(匹配量将只是两者中较小的一个)。

这是一个非常令人满意的问题，实际上也很有趣。启动一个计时器，这将是另一种完全不同的体验。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*