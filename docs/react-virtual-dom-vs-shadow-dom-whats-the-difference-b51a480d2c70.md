# React 虚拟 DOM vs 阴影 DOM:有什么区别？

> 原文：<https://javascript.plainenglish.io/react-virtual-dom-vs-shadow-dom-whats-the-difference-b51a480d2c70?source=collection_archive---------2----------------------->

## React 和 Vue.js 使用虚拟 DOM 来优化性能。那么什么是影子王国呢？

如果您使用 React 或 Vue，您可能会熟悉虚拟 DOM(文档对象模型)。这不应该与影子 DOM 混淆。

![](img/355ab20d6c7113a94d2beeacc2075326.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在看虚拟 DOM 和影子 DOM 之前，你应该对文档对象模型有一个清晰的了解。

为此，通俗地说，我们会说

> DOM 代表了你的网站的结构。

如果你想知道更多关于 DOM 是在哪里创建的，以及 HTML、DOM 和 JavaScript 之间的关系，可以考虑阅读[什么是 DOM？](/what-is-dom-in-javascript-c95531731367)

现在我们对 DOM 有了一些了解，让我们看看什么是虚拟 DOM。

# 什么是虚拟 DOM？

简而言之，虚拟 DOM (VDOM)是一个编程概念，其中 UI 的理想或“虚拟”表示保存在内存中，并通过库(如 reactjs.org[的 react DOM](https://reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom))与“真实”DOM 同步。

换句话说，React 构建了一个逻辑树来表示实际的 DOM 结构。

## 为什么我们需要虚拟 DOMs？

虚拟 DOM 是解决现代网络中常见问题的一种方式。

随着应用程序变得越来越大，框架和库往往过于频繁地操作和更新 DOM。这在很多方面都很昂贵。

浏览 DOM 变得更慢，需要更多的处理能力，最终会影响应用程序的性能。

例如，它可以使页面变慢。

有几种方法可以解决这个问题:

*   React 使用一个虚拟 DOM，并通过协调过程将其与真实 DOM 同步。
*   Angular 使用一种[变化检测](https://angular.io/guide/change-detection#angular-change-detection-and-runtime-optimization)机制“来查看你的应用程序状态是否已经改变，以及是否有任何 DOM 需要更新”。
*   Vue 也使用虚拟 DOM。通过使用一些 diff 算法，Vue 避免了在新的更改之后重新呈现整个 DOM。

简而言之，让我们记住虚拟 DOM 是真实 DOM 的副本。

通过告诉 React 我们想要实现的最终 DOM 状态(UI 应该是什么样子)，React 确保 DOM 匹配那个状态。

# 什么是影子 DOM？

影子 DOM 是一种为封装而设计的浏览器技术，例如，将标记结构、样式和行为隐藏起来，并与页面上的其他代码分开，以便不同部分不会冲突。

封装隔离了一些代码，使其不会与页面上的其他代码冲突。

![](img/2d4e83635dea1bd5a115253ebbaf64ff.png)

Photo by [Nick Tiemeyer](https://unsplash.com/@nickeedoo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

换句话说，由于影子 DOM，我们可以将其他元素附加到真正的 DOM 上，知道新元素不会与真正的 DOM 本身冲突。

由 [MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM#high-level_view) 提出的一个例子是`<video>`标签。虽然在 DOM 中只看到了`<video>`标签，但是这个元素在其 shadow DOM 中包含了一系列按钮和其他控件。

# 虚拟 DOM 和影子 DOM 的区别

关于虚拟 DOM 和影子 DOM 的区别可以说些什么？有点像 Java 和 JavaScript 的区别！

尽管提到了 DOM，虚拟 DOM 和影子 DOM 是不同的技术。

React 和 Vue 等库使用虚拟 DOM 来解决在保持最佳性能的同时更改 DOM 的问题。

虚拟 DOM 是整个真实 DOM 的副本，在浏览器 API 之上实现。

影子 DOM 是 web 组件和浏览器 API 所固有的。因此，在使用 React 和 Vue 之类的库或 Angular 之类的框架时，也可以使用它。

影子 DOM 是“隔离”在自己的 web 组件中的一部分 DOM。

相比之下，如果使用普通 JavaScript 创建应用程序，就不会使用虚拟 DOM。

[](https://medium.com/@lorenzozar/membership) [## 通过我的推荐链接加入 Medium-Lorenzo Zarantonello

### 如果这个有价值，直接支持我！我的文章大多是免费的。考虑成为会员以示支持…

medium.com](https://medium.com/@lorenzozar/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****