# 实现无限滚动的 3 种方法

> 原文：<https://javascript.plainenglish.io/3-ways-to-implement-infinite-scroll-7b2b7e47d58d?source=collection_archive---------7----------------------->

![](img/9d6fd5f47436e91d13d73a6ab3eed406.png)

Photo by [Veenit Panchal](https://unsplash.com/@veenit_panchal?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无限滚动(Infinite scroll)通常用于社交媒体和新闻提要，是一种 web 设计模式，允许用户连续滚动项目列表，当用户到达页面底部时加载新项目。

使用无限滚动，用户不需要单击分页按钮或导航到新页面来查看更多项目。相反，他们可以简单地向下滚动页面，新的项目将自动加载。

在这篇文章中，我们将使用 3 种不同的方法来实现无限滚动，并分析每种方法的优缺点。

# 1.使用`scroll`事件

`[scroll](https://developer.mozilla.org/en-US/docs/Web/API/Element/scroll_event)` [事件](https://developer.mozilla.org/en-US/docs/Web/API/Element/scroll_event)是每次滚动元素时触发的 DOM 事件。除了实现无限滚动，您还可以使用它根据滚动位置更新元素的布局或样式。

下面是一个使用`scroll`事件的实现:

Infinite scroll implementation using `scroll` event

## 优点:

*   **简单:**使用`scroll`事件是一种简单的方法，很容易实现。
*   **广泛支持:**所有现代浏览器都支持`scroll`事件，所以不需要担心兼容性问题。

## 缺点:

*   **糟糕的性能:**使用`scroll`事件可能是低效的，因为它在每次滚动事件时都会被触发，而不管用户是否已经到达页面底部。这对于包含许多元素的大型页面来说尤其成问题，因为它必然会导致性能问题。
*   **不用户友好:**使用`scroll`事件可能不太用户友好，因为它不能为用户提供流畅、连续的体验。当用户滚动时，内容被分块加载，这可能会很不协调。

# 2.使用`wheel`事件

`[wheel](https://developer.mozilla.org/en-US/docs/Web/API/Element/wheel_event)` [事件](https://developer.mozilla.org/en-US/docs/Web/API/Element/wheel_event)是一个 DOM 事件，当用户使用鼠标滚轮、触摸板或其他滚动设备与可滚动元素交互时被触发。`wheel`事件比`scroll`事件更高级，提供了更多关于滚动的详细信息。

Infinite scroll implementation using `wheel` event

## **优点**

*   **更好的性能:**使用`wheel`事件比使用`scroll`事件更有效，因为它只在用户与页面交互时触发，而不是在每次滚动事件时触发。这对于包含许多元素的大型页面尤其有用，因为它可以提高页面的性能。
*   **用户友好:**使用`wheel`事件可以为用户提供更流畅、更连续的体验，因为内容是在用户滚动时加载的，而不是成块加载的。

## 骗局

*   **复杂:**使用`wheel`事件实现无限滚动可能比使用`scroll`事件更复杂，因为您需要处理不同类型的用户输入(例如，鼠标滚轮、触摸板等)。)并确保无限滚动在不同设备间表现一致。
*   **可能无法在所有浏览器上工作:**`wheel`事件仍然不被所有浏览器支持，因此您可能需要包含一个 polyfill 来支持旧版本的浏览器。

# 3.使用 IntersectionObserver API

[intersection observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)允许您监控一个元素与其祖先元素或顶级文档的视图的交集。它非常适合实现无限滚动等功能。

Infinite scroll implementation using IntersectionObserver API

## 优点:

*   **最佳性能:**intersection observer API 允许您异步监视元素与视口的交集，而无需不断轮询滚动位置。这比其他方法更有效，尤其是对于包含许多元素的大型页面。
*   **可定制:**intersection observer API 允许您定制触发交集的阈值以及交集所关联的根元素。这对于微调无限滚动的行为很有用。

## 缺点:

*   **可能无法在所有的浏览器上工作:**即使 IntersectionObserver API 现在在大多数浏览器的最新版本中都得到支持，所以如果您需要支持旧版本的浏览器，您可能需要包含一个 polyfill。

# 结论

在 web 应用程序中实现无限滚动可以增强用户体验，本文中介绍的每种方法都有其优点和缺点。最佳方法取决于应用程序的特定需求和要求。

感谢您的阅读，希望这篇文章对您有所帮助。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*