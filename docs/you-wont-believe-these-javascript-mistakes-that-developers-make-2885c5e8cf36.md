# 你不会相信开发人员犯的这些 JavaScript 错误

> 原文：<https://javascript.plainenglish.io/you-wont-believe-these-javascript-mistakes-that-developers-make-2885c5e8cf36?source=collection_archive---------2----------------------->

## 一开始我也不相信他们。

![](img/b9ca5bd282dfd9346aba99c47cf06c86.png)

Photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我是 JavaScript 的忠实粉丝，我想我对它非常了解。然而，在我看来，我抛出了我在浏览开源代码时看到的最常见的错误，比如:

1.  **沉迷于异步**。是的，好的，不妨碍执行是极好的。但是，您必须知道如何管理异步软件，尤其是如果您没有创建一个简单的工具来响应外部调用的话。对于许多应用程序，最好关注功能及其结果，并对同步保持冷静。但是，也会有头疼的事情。
2.  **在实践中混淆数组和散列(对象)**。来自 PHP 的一些人偶尔会包装起来编写软件，只因为 JavaScript 很灵活，但是最终还是会出现 bug。
3.  **使用外部库来编写同样的东西，并为你的项目进行优化。**一个库不知道有什么错误处理，也不知道如何处理异常情况(例如，null/undefined/= =和===之间的差异)。最好只在它们是标准的并且用于复杂函数时才使用它们(所以 Express 是可以接受的)。
4.  **文笔不好，晦涩难懂。**这不仅仅是 JavaScript 的问题，但是对于 JavaScript，由于缺少输入和编写相同内容的 200 种方法，一切都变得更加黑暗。似乎有一个编写代码的竞争已经变得模糊不清了。
5.  **不要利用承诺。**我们在 2022 年。一切都是承诺:主要的框架都使用它们，甚至 jQuery，当您调用 ajax 时，也会返回一个承诺。它们简化了代码的可读性，通常也简化了工作流程。
6.  **不写 ES。**我理解你可能害怕兼容性，但是一个任务跑者加巴别塔就足够解决了。此外，各种 EcmaScripts 中的新奇功能使您的生活更加轻松。
7.  **不要使用正确的库。**你有多少次需要映射模型来调用 rest？有骨气。需要关于对象和数组的帮助吗？洛达什可以帮你。这样会减少你的努力，对其他程序员来说更清晰。
8.  **不认为对象相关。**这也是 PHP 的一个典型问题，但只要你只需要使用原型，我就差不多明白了。尽管如此，ES 已经用许多扩展和构造函数实现了这些类，所以没有更多的借口。
9.  **不用担心兼容性。如上所述，兼容性可能会让你害怕，但是你不必忽视它或者落后于技术。一些研究就足够了。CSS 也是如此。**
10.  混合了太多的框架/库。经常发生，太经常了。所以，朋友们，如果你用 React/Angular/Vue，请不要也用 jQuery。我理解有时候插件可能需要它们，但是版本通常会适应前面提到的框架。
11.  **不追赶。**这适用于所有语言，很抱歉这么说，但如果你想做一个前端开发人员，却连一个框架都不懂，不知道如何使用 npm，你是不会走远的。

[](/i-asked-senior-programmers-about-the-kind-of-programmers-that-annoy-them-at-work-c24dd1272b73) [## 我向高级程序员询问了在工作中让他们烦恼的程序员

### 看看你是否能理解他们。

javascript.plainenglish.io](/i-asked-senior-programmers-about-the-kind-of-programmers-that-annoy-them-at-work-c24dd1272b73) [](/my-boss-didnt-want-to-hire-experienced-developers-for-several-reasons-982252bcca12) [## 出于几个原因，我的老板不想雇用有经验的开发人员

### 这激怒了我，侮辱了我们作为开发者的种族。

javascript.plainenglish.io](/my-boss-didnt-want-to-hire-experienced-developers-for-several-reasons-982252bcca12) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*