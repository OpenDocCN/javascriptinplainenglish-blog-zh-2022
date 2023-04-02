# 不要再用 JavaScript 定时器了！

> 原文：<https://javascript.plainenglish.io/stop-using-javascript-timers-for-that-2e5ce83cb99c?source=collection_archive---------5----------------------->

## 这里有 JavaScript 中定时器的五种反模式以及如何正确使用。

![](img/c1f6179a06e70319304629f07b938757.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

现代 web 开发面临许多来自异步方面的挑战。在 JavaScript 中，我们倾向于使用定时器来处理其中一些。我说的计时器是指 setTimeout 和 setInterval。然而，大多数时候，这并不是一个好主意，因为定时器不是高性能的，可能不会按照我们希望的方式运行。在本文中，我将解释一些定时器的行为，并描述定时器是反模式的场景以及应该首选哪些解决方案。

一般来说，我们可以说定时器是用来轮询信息的。轮询是获取新数据的两个编程概念之一。使用轮询，我们不断地询问数据源是否有特定值的更新。另一方面，推送概念会在我们关心的事情发生变化时通知我们，然后我们可以对其做出反应。如果您不熟悉这些技术，您可能会认为推送是一个我们可以监听的事件，而轮询是一个循环，只有当数据源发生变化时才会返回值。推送通常优于轮询。

## 链式计时器

在 JavaScript 中链接计时器是可能的。使用定时器时，理解链接的概念是很重要的。看一下下面的例子:

```
let i = 0;
setInterval(() => console.log(++i), 100);
```

这将记录 1 2 3 4 5 …等等。输出将*保持在顺序*中，因为在我们的定时器中声明的函数的执行是以正确的顺序链接的，并且我们可以依赖于被一个接一个执行的链。虽然，我们不知道两次处决之间的时间。我们只知道至少是 100ms。但是正如我们将要学习的，上面的例子甚至可以花五分钟(！)直到它被执行——即使我们没有在代码中做任何其他事情(例如，即使我们没有将一个长时间运行的操作链接到计时器)。

setTimeout 也是如此:

```
let i = 0;
const myTimer = () => {
  setTimeout(() => {
    console.log(++i);
    myTimer(); // <- chain another timer
  }, 100)
}myTimer();
```

这将产生相同的输出。

## JavaScript 计时器和性能

计时器会在每次运行时唤醒 CPU。setTimeout 和 setInterval 本质上不是 CPU 密集型的，但是它们运行的函数可能是 CPU 密集型的。因此，使用计时器可能是个坏主意，这取决于你希望计时器运行的频率。根据经验，每秒多次运行你的定时器可能不是一个好主意，尤其是在低端移动设备上。此外，不要依赖你的计时器被及时执行。特别是当你的用户离开时，你不能依赖你的定时器在给定的时间间隔内执行。浏览器会调节计时器以节省能量。

## JavaScript 计时器和节流

对于不同的浏览器，以下内容可能会有不同的处理方式。然而，在这一章中，我们将只关注 Chrome。差异应该很小，可能主要适用于“可见页面”的定义通常，隐藏页面是最小化的或者不在活动标签中的页面。但是浏览器可能决定当一个页面的内容完全不可见时，它也是隐藏的。您可以使用页面可见性 API 来检查何时触发了可见性更改([https://developer . Mozilla . org/en-US/docs/Web/API/Page _ Visibility _ API](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API))。

Chrome 决定何时以及如何在不同阶段调节计时器:

**第一阶段:最小节流**

当满足以下条件之一时，将应用最小限制:

*   页面可见。
*   页面在过去 30 秒内“发出噪音”。在 Chrome 中，当这种情况发生时，你的标签会在标题旁边显示音频图标。静音音频不算。

除非超时少于 4 毫秒，并且 100 个或更多计时器被链接，否则计时器不会被限制。在这种情况下，超时设置为 4 毫秒。

注意:Chrome 中 100 个链式计时器的限制是新的。以前，只有五个计时器。

**第二步:介质节流**

当最小限制不适用并且满足以下任一条件时，浏览器会这样做:

*   链计数小于 100。
*   页面隐藏了不到五分钟。
*   页面使用 WebRTC。这意味着存在打开的 RTCPeerConnection 或实时 MediaStreamTrack。

链中的计时器将每秒检查一次。因此，不同链中可能会有重叠的计时器。这些函数将被批处理，然后执行。

**第三步:密集节流**

如果最小或中等限制都不适用，并且以下所有*条件均为真，则密集限制将到位:*

*   *页面已隐藏超过 5 分钟。*
*   *链计数大于 100。*
*   *该页面至少有 30 秒没有播放音频。*
*   *没有使用 WebRTC。*

*在这种情况下，浏览器将每分钟检查一次计时器。不同组的重叠计时器将被批量执行。*

## *JavaScript 中带有计时器的常见反模式*

*既然我们已经弄清楚了一些关于计时器的事情以及它们可能如何被抑制，那么让我们来看看一些反模式以及如何避免它们。*

***检查一个元素是否在视窗中***

*您可以使用 IntersectionObserver 来检测当前视口中的元素([https://developer . Mozilla . org/en-US/docs/Web/API/Intersection _ Observer _ API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API))。这将是一个触发的事件，而不是轮询，您可以对其做出反应。*

*跨计时器的交叉观测器的常见用例有:*

*   *页面滚动时延迟加载内容(还要考虑图像的 loading 属性)。*
*   *当元素进入视图时运行任务(例如，应用样式)*

*在上面的文章中提到了更多的用例，但是你以前可能不会使用定时器来解决这些问题。*

***检查一个元素是否改变了它的大小***

*与前面的例子类似，我们可以利用 ResizeObserver 来检查元素是否改变了维度([https://developer . Mozilla . org/en-US/docs/Web/API/resize observer](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver))。*

*ResizeObservers 的常见用例有:*

*   *实现每个元素的媒体查询来强制定义断点和样式。*
*   *保持滚动位置:当您不想混淆用户并保持他们在列表中的当前滚动位置时，即使项目样式正在改变(由于媒体查询)，您也可以利用 ResizeObserver 来调整滚动位置。*

***检查 DOM 是否已更改(添加/删除元素)***

*这是我时常看到的一个反模式。应该避免使用计时器来检查 DOM 中是否存在某个元素。*

*相反，您可以使用 mutation observer([https://developer . Mozilla . org/en-US/docs/Web/API/mutation observer](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver))作为推送替代。如果您正在处理的是一个定制元素，您可能能够使用定制元素的生命周期事件([https://developer . Mozilla . org/en-US/docs/Web/Web _ Components/Using _ custom _ elements # Using _ the _ life cycle _ callbacks](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements#using_the_lifecycle_callbacks))。*

*变异观测器的常见用例有:*

*   *检查是否在 DOM 中添加或删除了元素。*

*但是，要小心！许多像 React 这样的库可以用他们的工具解决这个问题。因此，当您不使用普通 JavaScript 时，您可能不需要 MutationObserver。*

***观察一般状态***

*不要使用 setInterval 或 setTimeout 来观察状态。例如，不要使用 setInterval 来检查变量的值是否已经更改。有更好的方法来解决这样的问题。例如:*

*   *把你想观察的数据包装在一个代理中([https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy))。*
*   *使用承诺。*

***一般动画***

*动画不应该不必要地唤醒 CPU。因此你不应该使用定时器来触发动画。更好地创建动画使用这些:*

*   *CSS 动画*
*   *网页动画 API([https://developer . Mozilla . org/en-US/docs/Web/API/Web _ Animations _ API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API))*

*CSS 动画和动画 API 将确保动画只在设备可以显示的帧上计算。使用 JS 中的定时器，你可能会在设备不能画出的中间帧中计算函数。*

*除此之外，使用 API 预先声明的动画可以由浏览器进一步优化。例如自动合成。*

*如果你的动画帧速率很低，你仍然可以使用定时器。为了确保您只在设备可以渲染的帧上绘制，您仍然应该将计时器解决方案与`requestAnimationFrame`结合使用。*

***来自服务器的轮询信息***

*除了从服务器轮询信息(例如，获取 setInterval 以检查新数据)，您还可以使用以下方法之一(顺序是任意的):*

*   *Web sockets
    https://developer . Mozilla . org/en-US/docs/Web/API/Web sockets _ API*
*   *SSE
    [https://developer . Mozilla . org/en-US/docs/Web/API/event source](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)*
*   *推送消息
    [https://developer.mozilla.org/en-US/docs/Web/API/Push_API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)*
*   *获取流
    [https://developer . chrome . com/articles/fetch-streaming-requests/# previous-on-the-exciting-adventures-of-fetch-Streams](https://developer.chrome.com/articles/fetch-streaming-requests/#previously-on-the-exciting-adventures-of-fetch-streams)*
*   *https://grpc.io/ RPC
    T22*

*最初的文章和想法来自杰克·阿奇博尔德，最初写在这里:[https://developer . chrome . com/blog/timer-throttling-in-chrome-88/](https://developer.chrome.com/blog/timer-throttling-in-chrome-88/)*

*我更新了一些信息，因为这篇文章已经有点旧了。请注意，本文提到了触发节流的链限制为 5。这不再适用于 Chrome(自 2022 年 8 月 2 日起，Chrome v104)。*

*就这些了，伙计们！*

*如果你喜欢阅读更多这样的文章，请随意留下评论或回复——这样，我就可以看到每篇文章获得了多少关注，以及我接下来应该写些什么。*

*非常感谢！*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。****