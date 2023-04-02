# 三原则——三振出局，你就重构

> 原文：<https://javascript.plainenglish.io/rule-of-three-three-strikes-and-you-refactor-942d13e7d5cd?source=collection_archive---------2----------------------->

## 在删除重复的代码之前，请三思

![](img/04f70d93e901b6cba7862b041452915f.png)

Photo by [Joao Tzanno](https://unsplash.com/@jtzanno?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

软件开发中最常见的一个误区就是**干原则——不要重复自己**。这通常听起来很简单:[DRY 原则](https://medium.com/@mariusbongarts11/dry-your-wet-typescript-code-e3c777b3daf9)指出，应该避免在存在于两个地方并重复相同知识和业务逻辑的代码中出现重复和重复。实际上，即使是有经验的开发人员也不会意识到代码复制和知识复制的区别。

对于有经验的开发人员来说，认识到**知识**和**意外复制**之间的区别甚至更加困难，因为需要对代码的领域理解。

# 知识复制

> *“我们看到的是语法重复还是知识重复？”—安东尼·夏马纳*

为了从根本上发现知识重复，必须肯定地回答两个问题:

1.  ***是否存在看起来完全相同的代码？***
2.  ***代码是否重复相同的知识和逻辑？***

回答第一个问题很容易。假设您使用正则表达式来验证密码强度:

在应用程序的其他部分，我们初始化同一个变量。显然，存在看起来完全相同的代码。

1.  *确实存在看起来和✅一模一样的代码*

**但是，代码是否重复了相同的知识和逻辑？**这个问题比较难。如果不确定，可以问一个替换问题:*改变一个代码块会导致改变另一个吗？*

> 存在真正的复制，其中对一个实例的每一个改变都需要对该实例的每一个副本进行相同的改变。——罗伯特·马丁

我有意识地选择了一个简单的例子。假设验证密码的正则表达式用于相同上下文中的相同应用程序，如果逻辑发生变化，我们需要在两个地方更改代码。这意味着我们的应用程序重复相同的知识。

*2。代码重复着同样的知识和逻辑* ✅

由于两个条件都适用，我们可以确认代码中的知识重复。我们可以通过删除重复的代码来重构我们的代码。

也许，你已经意识到回答第二个问题并不容易。我们需要理解应用程序的底层业务逻辑，以避免删除**意外的重复**。

# **意外重复**

为了理解意外复制，让我们看一些示例代码:

让我们再次检查我们的问题:

1.  ***是否存在看起来完全相同的代码？***
2.  ***代码是否重复相同的知识和逻辑？***

和第一个例子一样，这段代码包含一些重复的语法。`ProductService`和`FeedbackService`都在重复这个代码块:

我们可以很容易地将这段代码外包给抽象超类`CRUDService`。这将为我们节省几行重复的代码。

1.  *确实存在看起来和✅一模一样的代码*

现在，关于第二个问题。让我们从提出替换问题开始:*改变一个代码块会导致改变另一个代码块吗？*

假设我们的业务逻辑发生了变化:

> ***现在每个用户都可以创建反馈，但创建产品仍需要拥有适当的权限。***

这将导致我们改变`FeedbackService`类，但`ProductService`类不需要改变。这意味着我们发现了**偶然的重复**，我们不应该抽象我们的代码。

*2。代码不重复相同的知识和逻辑* ❌

> *“如果两个明显重复的代码段沿着不同的路径发展——如果它们以不同的速率变化，并且出于不同的原因——那么它们不是真正的重复”——罗伯特·c·马丁*

想象一下，通过清理重复的代码来抽象我们的代码，不仅我们的两个示例类继承了我们的超类，还有更多。因为我们清理了意外的重复，所以我们已经取消了代码的重构。这比拥有一些重复的代码要糟糕得多。

理论上，我们现在应该能够区分必要的和偶然的复制。

但是如果我们不确定呢？

# 三法则

> *三振出局，你重构*

发现知识重复并不容易，清理意外重复远比复制代码更有害。

三 3️⃣法则定义了当你发现一些重复的代码并且前两种情况不足以识别共享的知识时，**在你重构之前等待第三个重复的**。

> *真的很难，感觉很可怕，但还是闭上眼睛试试吧。——*[*贾斯汀·维斯*](https://www.justinweiss.com/articles/i-dry-ed-up-my-code-and-now-its-hard-to-work-with-what-happened/)

马丁·福勒在他的书*中定义了三条规则:重构:改进现有代码的设计:*

*   第一次做某件事，你就去做。
*   当你第二次做类似的事情时，你会因为重复而退缩，但你还是做了同样的事情。
*   *当你第三次做类似的事情时，你就重构了。*

# 最后的想法

重复代码是软件中技术债务和错误的主要原因之一。这就是为什么 DRY 原则是软件开发中最有价值的原则之一。但是，正确应用它更为重要。

记住，每当你发现 dome 重复的代码时，问问自己:*“我看到的是重复的语法* *还是重复的知识* *？”。*如果你不确定，应用三的**法则。**

我希望你喜欢阅读这篇文章。我总是很乐意回答问题，也乐于接受批评。请随时联系我😊

这里是无限制访问媒体上所有内容的链接。如果你用这个链接注册，我会赚一小笔钱，不需要你额外付费。

[](https://medium.com/@mariusbongarts/membership) [## 通过我的推荐链接加入 Medium-Marius bong arts

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@mariusbongarts/membership) 

关注我，不要错过我的下一篇文章。我写了关于 Typescript、Web 组件、前端框架、软件设计模式、Chrome 扩展以及更多的主题！🙏

# 关于作者

Marius Bongarts 是埃森哲互动公司的软件工程分析师。他还创建了 [Web Highlights Chrome 扩展](https://chrome.google.com/webstore/detail/web-highlights-%20-bookmark/hldjnlbobkdkghfidgoecgmklcemanhm)，允许成千上万的用户在每个网站上创建文本亮点和书签。通过提供标签和目录，您可以在 web-highlights.com 上的相应网络应用程序中轻松地重新找到您的网络研究。看看吧！

通过**[**LinkedIn**](https://www.linkedin.com/in/marius-bongarts-6b3638171/)**与我取得联系或者在 [**Twitter**](https://twitter.com/MariusBongarts) 上关注我。****

****[](https://medium.com/@mariusbongarts11/will-web-components-replace-frontend-frameworks-535891d779ba) [## Web 组件会取代前端框架吗？

### 它们是为解决不同的问题而构建的。

medium.com](https://medium.com/@mariusbongarts11/will-web-components-replace-frontend-frameworks-535891d779ba) [](https://medium.com/@mariusbongarts11/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [## 我的第一个 9.99 美元之旅与我的副业

### Chrome 扩展带来的被动收入

medium.com](https://medium.com/@mariusbongarts11/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [](/publish-your-side-project-now-1e3bb170c079) [## 发布你的副业，现在！

### 如果你不为你的第一次发布感到尴尬，那你发布得太晚了。

javascript.plainenglish.io](/publish-your-side-project-now-1e3bb170c079) 

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*追随我们。加入我们的* [***社群不和***](https://discord.gg/GtDtUAvyhW) *。*****