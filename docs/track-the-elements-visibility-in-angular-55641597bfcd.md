# 如何以角度跟踪元素的可见性

> 原文：<https://javascript.plainenglish.io/track-the-elements-visibility-in-angular-55641597bfcd?source=collection_archive---------5----------------------->

## 跟踪元素可见性的另一种方法。

![](img/e546ce4f6ea4c1c3ab4d534c34439ce8.png)

Business cartoon vector created by pch.vector — [www.freepik.com](http://www.freepik.com)

在过去，跟踪元素的可见性并不是一项简单的任务。常见的解决方案之一是监听文档滚动事件，并通过`Element.getBoundingClientRect()`检查元素的可见性。它有两个主要缺点:

*   它是 CPU 密集型的
*   计算在主线程中运行，导致滚动缓慢

幸运的是，浏览器供应商创造了一个高性能的替代品，并且有一个简单明了的使用 API。

# 交叉点观察器 API

[交集观察者 API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 是一种异步观察元素可见性的方法。所有的计算都在后台线程中完成，这意味着用户体验尽可能保持流畅。

为了使用交叉点观察器，我们基本上需要两样东西

*   IntersectionObserver 实例
*   我们要跟踪的元素

其他一切都是配置的问题，你可以在[文档](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)中读到。

假设我们想要跟踪 id 为“product”的元素，并在它出现在视口中时得到通知:

我们正在执行以下步骤:

*   获取产品元素
*   创建观察者实例并传递回调，每次更改时都会调用该回调
*   我们正在遍历条目列表。条目是一个列表，而不是一个对象，因为您可能在多个元素上使用同一个 IntersectionObserver
*   我们正在记录元素可见性
*   最后，我们调用 observe 方法来监听变化

# 角度进场

我们可以创建一个通用指令，在元素可见性改变时发出一个事件，而不是使用 IntersectionObserver。它可能是这样的:

代码是不言自明的，所以我不会过多地描述它，我唯一要注意的是，我们正在 JS 区域外运行 Intersection Observer。根据我的经验，大多数时候我把这个指令用于像 Google Analytics 这样的监控工具，在这些工具中，你不希望对每个观察到的变化都进行变化检测，此外，当你有一个庞大的列表需要观察时。尽管如此，这不是一件必须做的事情，只要适合你…

请记住，我们正在断开与`ngOnDestroy`上的观察者的连接，以避免内存泄漏。

现在你知道了。感谢您的阅读。

*更多内容看* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*