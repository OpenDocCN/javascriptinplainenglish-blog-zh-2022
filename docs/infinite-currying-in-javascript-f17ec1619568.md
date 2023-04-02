# JavaScript 中的无限奉承

> 原文：<https://javascript.plainenglish.io/infinite-currying-in-javascript-f17ec1619568?source=collection_archive---------3----------------------->

## 如何在 JavaScript 中实现无限 currying 的教程。

![](img/600555c520aef334218a5e5614da0d9d.png)

Photo by [Sam McGhee](https://unsplash.com/@sammcghee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

嗯，有一天天气很好，我正在面试前端开发人员的职位，在整个讨论过程中，我遇到了一个问题，我必须开发一个类似这样的功能。

`console.log(sum(1)(2)(3)(4)(5)(6)());`

基本上，这是一个可以对 n 个数求和的函数。第一个想到的就是“这是在拍马屁”。所以我试图做一个硬编码的解决方案，它将返回一系列等待下面输入的函数。

但是代码看起来很丑，而且是硬编码。再多的争论也无济于事。它只能达到 3 个论点的目的。那么，我们怎样才能让这段代码对一个程序员来说更通用、更有用，更重要的是怎样才能让面试官开心呢？

所以这里又出现了一个概念，让我们免于做重复性的工作。

## 递归

考虑一下在这个问题中我们如何实现递归。首先，我们必须考虑递归结束的基本情况。

总和(1)(2)(3)(4)(5)(6)……()

## 基础案例

正如我们在这里看到的，这个函数会一直持续到一个特定的条件，这个特定的条件是什么？当我们看到函数调用不再有参数时，我们将中断递归。当我们在没有更多参数的情况下进行调用时，即在最后一次调用()时，我们将返回总和。

否则，我们将不断返回一个函数，该函数将期望我们再用一个参数进行调用。

# 密码

Recursive Currying

这里，如果参数 b 存在，我们再次返回 sum 函数。让我们想象输入的递归`sum(1)(2)(3)()`。

1--返回 sum(1)

2--返回 sum(1+2)

3--返回 sum(1+2+3)

对于最后一个调用，我们没有参数 b，所以我们的函数返回 1+2+3。在前 3 次调用中，我们返回了内部函数，它可以容纳多一个参数。

如果这对你来说似乎很难，请不要担心，因为我第一次尝试时没有想到这个解决方案。我花了几分钟和面试官的暗示。我将链接一个视频来更好地解释这个话题，因为很难用文字来解释。

我也会向每个人推荐这个频道，因为他在他的频道上发布了真正有用的内容。

在这篇文章中，我们学习了无限 currying 及其在 JavaScript 中的实现。

*如果你明白我在这里说的任何事情，请鼓掌回应并跟随我，因为它帮助我保持动力并从我的日程中抽出时间来写这些文章。这不会花你任何钱，但会帮我很多忙*

高拉夫·夏尔马是一个狂热的读者和热情的旅行者。他试图通过传播他的知识和他的生活经历来过一个更有意义和目标的生活！跟随他踏上平衡数字生活和现实生活的新旅程。他住在印度的北阿坎德邦。他在 Instagram 上的[*@高尔夫。_.塞拉*](https://www.instagram.com/golf._.sierra/) *。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。****