# 如何用 useEffect 最大限度地减少加载次数

> 原文：<https://javascript.plainenglish.io/how-to-maximally-reduce-loading-times-with-useeffect-89f0f150bdba?source=collection_archive---------2----------------------->

## 用简单的设计模式重构 React 代码

![](img/6b4a8c6e7bdfb1130ea80eceb60c38e5.png)

Photo by [Christophe Hautier](https://unsplash.com/@hautier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/spinner?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近我一直在做两件事——重构大量的 React 代码和阅读软件设计模式。

在重构一些旧代码时，我一直在尝试让一些页面加载得更快。这就是问题所在——为了加载一个页面，我必须对不同的后端服务进行五六次网络调用。这实际上比旧代码要做的要多得多，因为后端已经被重新设计为使用微服务模式。

我没有读过太多这方面的内容，但我突然想到，或许切换到微服务驱动架构的一个代价就是这个！您的前端必须调用更多的服务来获得它需要的数据。

所以，如果你正在做前端的工作，你如何以一种简单且可重复的方式解决这个问题呢？

提示一个设计模式…看起来像这样:

这里的关键是第 16 行，它利用`Promise.all`异步运行所有不同的数据查询。然后，如果您只是在等待之后将您的`loading`状态设置为 false，那么您可以确保在所有不同的数据查询运行之后，您只将页面显示为已加载。

我还认为这是一种可读性很强的方法，因为你只需要在第 19 行的`useEffect`钩子中调用一个函数。我个人已经用这种模式重构了很多代码，并发现它确实有助于缩短加载时间，并使在单个 React 组件中进行多个后端调用变得非常容易，而事情不会变得复杂。

这里需要注意的一点是，我没有处理钩子的依赖关系。有很多不同的方法可以做到这一点，所以这超出了本文的范围——例如，您可以将函数包装在 useCallback 钩子中，或者将所有内容都放在 useEffect 钩子中。

所以我希望这是有用的🙂

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***