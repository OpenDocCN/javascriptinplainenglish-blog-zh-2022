# 用 requestAnimationFrame 改进了轮询 API

> 原文：<https://javascript.plainenglish.io/better-polling-api-in-react-with-requestanimationframe-983d02ff048?source=collection_archive---------1----------------------->

## `useRafPolling`自定义挂钩可以更好地做到这一点

![](img/25809d4012d74f3a848a74095aff0cca.png)

Photo by [Elliott Stallion](https://unsplash.com/es/@eagleboobs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 React 应用程序开发中，您可能需要轮询 API 来持续更新页面数据，那么我们可以简单地使用`useInterval`自定义钩子来完成这项工作:

但我认为它有两个不完美之处:

*   由于`setInterval`的特性，当用户将这个 Web APP 放在后台时，它也会不断轮询这个 API，但此时用户的注意力已经不在你的 Web APP 上了，这无疑是一种浪费，页面数据更新却无人问津，也消耗了用户的设备电量。
*   这个钩子对于同步回调来说很好，但是请求 API 是异步的。所以我们不能保证 API 返回的数据会很快到达，可能会因为各种网络原因延迟很久。也就是说，你设置的轮询间隔严格来说是针对后端服务轮询间隔，而不是更新你页面的间隔。

所以我准备写一个`useRafPolling`自定义钩子来解决这个问题:

首先我定义了一个`setRafTimeout`而不是`setTimeout`。这是因为`requestAnimationFrame`在 web 应用程序处于后台时暂停呼叫，这提高了性能和电池寿命。

然后我用`async...await`执行异步回调，然后开始计时。虽然这并不能保证页面数据更新的时间间隔，但是我们减少无用的重复 API 请求，保证每个请求都是有效的，数据是最新的。

此外，编码中还有两个提示点。一种是我们使用`RafHandle`来存储`requestAnimationFrame`每次返回的`id`，保证了在访问`timerRef`时能够检索到最新的`id`。第二，`endedRef`用来标识当前是否已经结束，因为当异步任务完成时，这个钩子可能已经被卸载或者`end`。从长远来看，如果 React 的状态在这个异步函数中被更新，那么您需要小心地确定当前组件是否已经被卸载。下面是一个完整的例子:

*不是中等会员？* [*支持我在这里成为一个*](https://medium.com/@hellostephanie2022/membership) *。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****