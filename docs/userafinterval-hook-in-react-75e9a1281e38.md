# React 中的 useRafInterval 挂钩

> 原文：<https://javascript.plainenglish.io/userafinterval-hook-in-react-75e9a1281e38?source=collection_archive---------4----------------------->

## 为什么不用`setInterval`，而用`requestAnimationFrame`

![](img/e2aba8950318906a43370b233944a75b.png)

Photo by [Alexander Shatov](https://unsplash.com/@alexbemore?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 React 中，我们可以为一些重复的逻辑使用定制的钩子。举个例子，如果我想写一个每隔一段时间执行一个同步函数的钩子，我可以这样写`useInterval`:

代码看起来很清楚，对吧？像这样使用:

```
const clear = useInterval(() => {
    setCount((c) => c + 1);
}, 1000);
```

但是`setInterval`会在用户电脑锁屏或者切换到另一个标签页时继续运行。这也意味着它在后台不断消耗你的设备的电池。我们可以使用`requestAnimationFrame`来代替，它告诉浏览器你希望执行一个动画，并请求浏览器在下一次重画之前调用一个指定的函数来更新动画。为了提高性能和电池寿命，在后台标签或隐藏 iframe 中运行时，大多数浏览器都暂停调用。

我们先写一个`setRafInterval`，就像`setInterval`一样:

接下来，只需替换`useInterval`中的`window.setInterval`，并简单调整类型:

以上是完整的代码。`requestAnimationFrame`通常是根据你的屏幕的刷新率来调用的，比如一个常见的`60HZ`屏幕，每秒回调的次数是 60 次，大概是`16.6` s，所以这里我们定义`RafHandle`，将每次调用返回的`id`存储在对象中。由于外部使用的对象的引用，当读取`id`时，您将总是获得最新的`id`。

下面是一个使用案例:

最后，由你来权衡这两个选项。比如你要做一个计时之类的后台运行的案例，或者你需要在小于`16.6` ms 的间隔内执行一个函数，那么`requestAnimationFrame`就不能选择，但是如果是一些计算更新动画等。，`requestAnimationFrame`明显更好。

*不是中等会员？* [*支持我在这里成为一个*](https://medium.com/@hellostephanie2022/membership) *。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***