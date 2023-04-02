# 4 个高品质定制反应挂钩

> 原文：<https://javascript.plainenglish.io/with-5-high-quality-react-custom-hooks-i-got-promoted-eafe77684ca8?source=collection_archive---------10----------------------->

## 下面是这 4 个 React 钩子如何不可思议地解放了我的生产力。我希望这能帮助你赚更多的钱。

![](img/5be3213b280beabf7a1162356ab028a2.png)

Photo by [Alexander Mils](https://unsplash.com/@alexandermils?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是自定义挂钩

*钩子是 React 16.8 中的新增功能。它们允许您使用状态和其他 React 特性，而无需编写类。*

有了自定义钩子，组件逻辑可以提取到可重用的函数中，我将根据实际使用场景列出这 4 个高质量的钩子。

## 通过这篇文章，你可以了解到

*   如何在不担心内存的情况下合理地请求数据
*   钩子形式的 DOM 滚动的高性能监控
*   告别样板意大利面代码，快速实现元素悬停的效果
*   快速创建高性能的动画弹出窗口，包括钩子、吐司和工具提示等。

# 1.使用安全状态

如果你在你的 React 应用程序中看到这个错误，请举手，✋:

*警告:无法在卸载的组件上调用 setState(或 forceUpdate)。这是不可行的，但它表明您的应用程序中存在内存泄漏。
要解决这个问题，请取消 componentWillUnmount 方法中的所有订阅和异步任务。*

为什么会出现这个问题？

当您发出一个**异步数据请求，但是组件已经被卸载**时，这个错误经常发生。例如，应用程序中的一些逻辑告诉 React 远离组件。

您仍然有一个针对远程数据的**未决请求**，但是当数据到达并修改组件状态时，应用程序已经呈现了一个不同的组件。

嗯，怎么解决？

有一个解决方案并不完美:

严格来说，你**没有取消你的数据获取请求**。变通办法检查组件是否已安装。如果组件没有安装，它会避免调用`setState`。但是网络请求仍然有效。

## 胡克溶液

怎么用？

跟我们一样，`useState`用法是一样的，但是组件卸载后，`setState`将不再执行异步回调，避免组件卸载后更新状态导致内存泄漏。

# 2.使用 IntersectionObserver

这个钩子是基于[intersect observer](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver)实现的，你可以在 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver) 上找到更多 intersect observer 配置。

如果元素在窗口中可见，则返回 true，并且只执行一次。

## 真实场景

有一个要求是，当屏幕滑动到底部某个元素时，我需要传递一些参数给服务器，以便更好地分析用户的产品使用情况，所以此时你可以使用这个钩子。

完了！使用方法很简单，没有问题！:)

# 3.使用悬停

这是一个我们经常使用的钩子，所以你不必写同样的`mouseenter`、`mouseleave`和`debounce`。

首先，您需要一个`useEventListener`钩子来快速注册和销毁事件:

然后，在`useHover`中，写鼠标进入和鼠标离开事件，它将返回一个`Boolean`值:

怎么用？

# 4.useDelayUnmount

嗯，你的项目里有以下动画吗？

![](img/e274d74160a1516ba6cd7559011e2460.png)

A modal, but no leaving the animation

首先，这个弹窗可以正常使用，有淡入效果，这是好的，但是从视觉层面来说，这个弹窗似乎缺少一种淡出动画效果。这是因为用户体验会更好，所以我们试着用 hook 来改造一下:

太神奇了！代码很简单，让我们制作一个完整的高性能的带渐隐的弹出窗口。

太好了！它看起来好多了，我们用最短的可能的方式来完成一个用户体验指标。

值得一提的是，react UI 库现在支持完整的高性能动画(组件被卸载)，这是一个好消息。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。**