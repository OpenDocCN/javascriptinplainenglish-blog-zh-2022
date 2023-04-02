# JavaScript 的 Async/Await 用简单的术语解释

> 原文：<https://javascript.plainenglish.io/javascripts-async-await-explained-in-simple-terms-5dfeb08665d4?source=collection_archive---------16----------------------->

## JavaScript 的 Async/Await 入门指南。

![](img/045226015e9cf56d7be5eb3632102028.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的异步意味着你的代码、应用程序能够在后台运行，而你看不到它，也不会阻止应用程序的其他代码或功能在后台运行。这听起来是不是太抽象了？这里有一个更进一步的解释。

你登录了一个电子商务网站，挑选了一件漂亮的 t 恤，然后点击了支付按钮。您输入您的卡的详细信息，然后等待付款确认。当你等待的时候，网站一直在后台运行，你可能会看到这样的信息，“请等待，我们正在处理你的付款”。或者您看到屏幕上有东西在移动，显示您的付款正在处理中。

上面显示了 async 的运行情况。它是一个应用程序在后台运行(从您的帐户中取钱)而不停止应用程序的其他功能(即“请稍候，我们正在处理您的付款”消息)的能力。

Async 函数和 await 关键字使程序员可以做到这些。值得注意的是，大多数时候异步操作都涉及到与第三方 API 的交互。

第三方 API 就像你使用别人提供的服务来帮助你的产品和服务。还记得电子商务网站吗？网站做的就是卖产品。它不是支付服务提供商。

然而，为了使在线支付更容易，电子商务商店通过将其电子商务商店链接到第三方支付服务(API)来使用第三方支付提供商。在您输入您的卡详细信息并点击“支付”后，在线商店运行到后台的第三方支付服务 API 以方便支付。电子商务商店只确认付款给你。

在本文中，您将学习如何编写一个异步函数并使用 await 关键字。

## **在**之前有一个**同步功能存在**

在异步函数和 await 关键字出现之前，JavaScript 使用“new XMLHttpRequest()”函数来执行异步操作。然后是“取”和“然后”。现在，异步函数。

XMLHttpRequest()过时且复杂。“获取”和“然后”很简单，但是写起来很长。几行代码更好。你的代码将是干净的，易于理解的。

在本文中，您将学习如何编写异步函数和使用 await 关键字。

## **如何用 JavaScript 写异步函数**

强烈建议您先学习如何用 JavaScript 编写函数。此外，您需要学习 JavaScript 中的模板文字。编写异步函数变得更加容易。

我们将使用一个第三方 API，它拥有关于世界各国的信息，比如人口、货币、语言等等。

让我们开始吧。

分解代码，第一行代码将所有代码存储在一个名为 getLocation 的变量中。然后开始异步动作，async 写在“function”这个词之前。这告诉代码在后台运行而不停止其他操作——您将在下面看到。然后在函数内部传递一个参数(国家)。

第二行将该行中的代码存储在“loading”中。这意味着该行中发生的所有事情都应该存储在“loading”中。“获取”关键字运行到第三方 API 网站[https://restcountries.com/v3.1/name](https://restcountries.com/v3.1/name)，以获取国家详细信息。如果您注意到了，模板文字引号(` `)和参数—国家—被模板文字符号(${ })包围在网站地址周围。“await”关键字意味着无论“fetch”方法得到什么，都应该在后台等待，不被任何人看到。

fetch 方法从第三方 API 返回的内容总是不可读的。下一行代码通过将响应转换为 JSON (JavaScript 对象表示法)使其可读。

下一行代码将结果记录在您的控制台中。最后一行调用 async 函数，并允许您在控制台中写入您想要获取其详细信息的国家名称。这里，我用了加纳。尝试使用你选择的任何国家。

在运行上面的代码之前，将下面的代码放在代码的最后一行，不要放在 async 函数中，以向您真正展示上面的代码是异步的。

像这样:

当您现在运行代码时，代码的最后一行首先记录在您的控制台中，而 async 函数获取您指定的国家(加纳或任何其他国家)的详细信息。

**附言** *作家面临的挑战可能会让他们终生无法写作……久坐导致的慢性背痛、长时间盯着屏幕导致的眼睛问题、写作时手指窒息等等。如果你想继续得到这种类型的文章，你可以成为* [*媒体订阅者来支持我。每月 5 美元。你的一部分订阅费归我*](https://sabitololade.medium.com/subscribe) *。*

*更多内容看* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**