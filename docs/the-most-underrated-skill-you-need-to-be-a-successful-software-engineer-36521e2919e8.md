# 成为一名成功的软件工程师所需的最被低估的技能

> 原文：<https://javascript.plainenglish.io/the-most-underrated-skill-you-need-to-be-a-successful-software-engineer-36521e2919e8?source=collection_archive---------7----------------------->

## 挫折承受力。

![](img/d5c9e1d873271565f35a180ab9b3585d.png)

Photo by [Cookie the Pom](https://unsplash.com/@cookiethepom?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

软件开发也意味着调试软件。所以最近我遇到了一个 bug，我被叫去处理，发现这个 bug 的开发人员在搜索了两个小时后就待命了。

与此同时，我发现错误取决于局部变量的数量。在汇编代码中，我可以看到这个 COM 对象的指针在微软库中被零覆盖，因此不再有效。

然后我打电话给我的经理。通过审查，我们发现了一个与症状不匹配的 bug，一般情况下不会发生，因为程序事先已经得到支持。一个小时后，他说他现在必须走了。他也没有回来。第二天，我被分配了 bug。

它最终是一个用错误的调用约定调用的函数，所以在返回时，该函数清理了堆栈，调用函数也是如此。稍后调用的 Microsoft Lib 函数覆盖了堆栈上的错误位置。

陷入这样的问题会非常令人沮丧，因为解决这个难题需要专门知识和技术来获得线索。因此，当我开始将未使用的局部变量打包到代码中时，从语义上讲，它不会改变期望的行为。

那么你为什么要这么做呢？

因为这样行为会改变，然后你会问自己这意味着什么。如果什么都没有改变，你的同事会看着你，不管那应该是什么废话。经验有助于进行这样的测试。获得这种体验会非常令人沮丧，可能要花上几天甚至几周的时间来搜索一个 bug。

我最长的 bug 搜索花了 8 周的全职时间。在这 8 周里，你不知道为什么一个项目突然结束，尽管你不能从项目文本中看出这一点。

8 周后，我写了一个详细的调试系统。不幸的是，错误只发生在我没有调试程序的时候。我称这个错误为[薛定谔的错误](https://en.wikipedia.org/wiki/Schr%C3%B6dinger's_cat),因为检查它纠正了错误，所以程序成功运行。

太令人沮丧了。然后你也考虑一下，是重写程序还是让它死掉。但是我想了解这个 bug。现在，更严格地处理我的 bug 搜索是我丰富经验的一部分。

你学得越多，你就越明白如何认真对待“未定义的行为”，即使它在当前的编译器版本下也能工作。你学会了欣赏和利用像一致性和多重继承这样的东西。这改变了关于软件架构的想法。

不幸的是我自己只有一个。我的大部分票都不是在 Bugzilla 做的。但是各自的同事已经放弃了，bug 还是要去。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**