# 用“switch(true)”而不是“if”——废话要赶时髦？

> 原文：<https://javascript.plainenglish.io/using-switch-true-instead-of-if-nonsense-to-be-trendy-6100401243b2?source=collection_archive---------1----------------------->

## 如果 switch(true)模式没有掩盖一个我很难注意到的问题，这篇文章就不会存在。有什么问题？

![](img/aaf2af577899238aeaf8515ec8fe7ad0.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

多年来，`if`和`switch`语句的使用一直是 JavaScript 社区争论和紧张的根源。许多研究表明，这两种说法之间没有实质性的性能差异。

也许这就是为什么大多数开发人员的行为与我相似，也就是说，他们根据情况使用两种语句中的一种。

例如，在这种情况下，我会一直使用`if`的说法:

然而，在这种情况下，我可能会使用`switch`:

这篇文章的目的不是要延长关于一个陈述是否更好地用作一个无止境的故事的争论。而且，从上面的例子中你可以看到，我并不是主张一种排他性的战略，而是主张一种包容性的战略。

此外，我尽可能使用“更干净”的模式，以避免高级模块依赖低级模块，这是`if`和`switch`语句的典型问题。

我在一个项目中合作过的一个中级 JavaScript 程序员的规则，出于某种原因，他用一个`switch`语句替换了大多数`if`语句，激励我写这篇文章。特别是因为在用“普通的”`switch`替换`if`语句比较棘手的情况下，它经常使用`switch(true)`模式。

Code example on StackBlitz

为了说明我的观点，考虑下面的任务——以下面的方式对带有数字键`id` (unique: 0 到(Array.length-1))和`value` (random: 0 到(maxValue-1))的对象数组进行排序:

*   *数组中有* `*id === 0*` *的成员总是先不管* `*value*`
*   *无论* `*value*`如何，带有 `*id === Array.length-2*` *的数组成员总是倒数第二*
*   *无论* `*value*`如何，带有 `*id === Array.length-1*` *的数组成员总是最后一个*
*   *数组的其他成员按* `*value*`排序

以下是使用`if`语句的解决方案:

这似乎是一段简单的代码。让我们看看如果使用`switch(true)`会是什么样子:

也许有人会觉得第二种选择更具可读性。我同意。如果这种模式没有掩盖一个我很难注意到的问题，一切都会好的，这篇文章也不会存在。有什么问题？

让我们先来解释一下`switch`语句是如何工作的。*(来源:*[*MDN*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch#description)*)*:

*一个* `*switch*` *语句首先对其表达式求值。* ***然后查找第一个*** `***case***` ***子句，其表达式的计算结果与输入表达式的结果相同(使用*** [***严格比较***](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators) ***、***`***===***`***)****并将控制转移到该子句，执行相关语句。(如果多个* `*case*` *与提供的值匹配，则选择第一个匹配的* `*case*` *，即使* `*case*` *彼此不相等。)*

这到底意味着什么？换句话说，当使用`switch(true)`模式时，它会在评估每个`case`子句后将其与 true 进行比较。这是这种模式中额外的、无意义但不可避免的比较。

如果将一个`switch(true)`语句“转换”成一个`if`语句，它会是什么样子？

是不是有点奇怪？

此外，由于这种无意义的比较，性能降低了 15%到 20%(使用`performance.now()`测量)。

在对一百万个数组成员进行排序时，可以在[示例](https://stackblitz.com/edit/react-ts-ccysj5?file=App.tsx)中看到这种性能下降，即使用`switch(true)`的解决方案几乎与使用不必要的`=== true`比较的`if`语句解决方案一样快。

做出自己的判断。由您和您的团队决定应用哪些编程模式，但是请记住您的决定对整个项目代码结构的影响，这些代码结构将作为遗留代码传递给未来的开发人员。

事实上，有些款式首先是流行的，然后才是实用的。这正是我对`switch(true)`模式的感受。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**