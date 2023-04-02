# JavaScript 程序员最糟糕的习惯

> 原文：<https://javascript.plainenglish.io/the-worst-habits-of-javascript-programmers-9bee8d86e7ab?source=collection_archive---------10----------------------->

## 认为它比实际情况简单。

![](img/314adc7e5534ce5fe19995695cd1b9c4.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

遵循博客和论坛中大量存在的简单规则，却不知道为什么(也不想冒犯，因为我重视那些坐下来回答 StackOverflow 上的问题的人的工作)

基本上，在你了解了语言的基本语法之后，你应该担心理解它背后发生的事情。因为这就是 JavaScript 中大多数错误的来源，没有很好地理解这种语言，因此认为它比实际上更简单。

在我看来，Kyle Simpson 的《你不知道 JavaScript》系列书籍应该是任何经常编写 Javascript 的人的必读之作。

在我看来，什么是良好的礼貌是很有争议的，因为根据你问谁，他们会回答不同的事情，这可能是因为我们倾向于通过更符合我们偏好的风格特征来塑造良好的礼貌。

我举几个例子:

*   你总是需要对代码进行评论。我可以说，需要注释才能被理解的代码应该重写，这样就不会了。就我个人而言，我发现花时间尽可能清晰地编写代码比解释它为什么如此复杂更有益。这似乎是一个很好的论点(对我来说，确实如此)，但是当你不能简化代码时，它不能作为不评论代码的借口。另一方面，我习惯于以标准的方式评论每个公共函数的用途以及它的参数是如何使用的。
*   在比较中你必须用===而不是==来代替。我们都听说过无数次了，但事实是，当您意识到您可能不应该比较不同类型的值，并且您担心这不会在您的代码中发生时，您理解 javascript 的强制规则(这比您想象的更重要和有用),因为它失去了许多效用并且是多余的
*   你必须用字母代替变量。更好的是，你必须使用 const 来代替 let 和 var。不管是谁告诉你，他已经完全失去了语言的视角，还是什么都没听懂，我不知道哪个更糟糕。

我不使用食谱，而是更喜欢将常识应用于每种情况，遵循一些对我来说像盒子一样的规则，这些规则适用于许多语言，而不仅仅是 JavaScript:

1.  **为人类而不是机器写代码。**如果你对此有异议，那就去学汇编吧，不要学高级语言。
2.  **按照偏好顺序编写清晰、一致、简洁的代码**。这是一个直接的结果，补充了规则 1。
3.  **尽可能避免**可能产生难以发现和/或解决的 bug 的**模式和习惯(即使只是在边缘情况下)。**
4.  如果你有一个好的借口，跳过上面的规则。但必须是好的！
5.  **全局定义变量**(有时候不是主动做的，是意外定义的；示例:确定闭包时)

尽管我们喜欢简单的食谱，但现实很少如此。我更愿意去理解它，而不是在场上装门，但每个人都有选择自己道路的自由。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***