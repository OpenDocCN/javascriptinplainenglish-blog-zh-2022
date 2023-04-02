# 2022 年，每个 JavaScript 开发人员都应该知道的一件事

> 原文：<https://javascript.plainenglish.io/1-thing-every-javascript-developer-should-know-in-2022-218fa6c2abc3?source=collection_archive---------0----------------------->

## 除非绝对必要，否则停止使用 if 语句。

![](img/7a7fa02b776512fd2cbbb49a23f60a86.png)

Photo by [Barney Yau](https://unsplash.com/@barneyyau?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coffee-focus?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

使用`if`语句是一种笨拙的编写代码的方式，应该尽可能避免(在大多数情况下，这几乎是 100%的时间)。

不要误会，`if`语句在某些场景下是有用的，并且是有原因的。然而，在可以避免它们的地方过度使用它们，不仅会使你在几个月后重访代码时更加困难，还会影响开发人员理解代码的上下文并继续完成分配给他们的任务所需的时间。这扰乱了“流动”,导致整体效率降低。少即是多。

查看下面的代码片段，我们通过加密的卡号从数据库中检索一张卡，并根据特定条件返回一个验证响应。

有这么多的`if`语句不仅需要相当多的努力来破译，而且随着更多条件的增加，我们很快就会上下滚动以确保每个情况都得到满足，这就火上浇油了。除此之外，出于可维护性的考虑，似乎还存在代码重复。

下面的例子就是这样做的。它用[逻辑 AND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND) 和[逻辑 OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR#short-circuit_evaluation) 代替了无数的 if 语句，更加简洁易懂。对于那些不熟悉析取和合取的人，我强烈建议去查一下，但这里有一个简短的描述:

*   **逻辑 AND** ( `&&`)从左到右计算操作数，立即返回遇到的第一个 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 操作数的值；如果所有值都为真，则返回最后一个操作数的值。
*   一组操作数的**逻辑 OR** ( `||`)运算符(逻辑析取)当且仅当其一个或多个操作数为真时为真。对于短路计算，它只返回第一个真值表达式。

随着业务需求的变化，代码也在变化。在某些情况下，这可能会完全删除代码，但在其他情况下，它会扩展到已经存在的内容。这里有一个常见的面试问题，它涉及到你创建一个可扩展的解决方案的能力:

> 创建一个函数，将 1-10 之间的给定数字转换成单词

简单吧？只要在函数中有一堆 if(或 switch)语句就可以了，给面试官留下深刻印象。

但是如果他们说，

> 要求变了。我们现在想使用这个函数将 1-100 之间的数字转换成单词

你现在打算做什么？继续为每一个场景写 if 语句？如果他们后来改变要求，将数字转换到 1000，那该怎么办？

更好的方法是从一开始就考虑一个可扩展的解决方案。在设计、架构、编写和维护代码时，要记住的一个关键的基本原则是时间如何影响软件的可持续性，以及如何使您的代码随着时间的推移而具有弹性。因此，可伸缩的解决方案是这样一种代码，其中要么没有任何`if`语句，要么只有几个语句可以覆盖大多数情况(如果不是所有情况的话),只需要很少的修改，甚至不需要修改。

最后，看看下面的片段，自己判断哪一个你认为是高度可扩展的、可维护的、更容易阅读的，并且如果你真的遇到它，将帮助你保持心流状态？

我之前的[文章](/4-coding-practices-ive-picked-up-working-for-a-startup-64cb92f001e0)展示了一个深入的可扩展前端解决方案，没有任何`if`陈述。一定要去看看！

[](/4-coding-practices-ive-picked-up-working-for-a-startup-64cb92f001e0) [## 我在创业公司工作时学到的 4 个编码实践

### 在公司的阶梯上向上爬不再依赖于你多年的经验。当然，这可能是一个决定性因素…

javascript.plainenglish.io](/4-coding-practices-ive-picked-up-working-for-a-startup-64cb92f001e0) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*