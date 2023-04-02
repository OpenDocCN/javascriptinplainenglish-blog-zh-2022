# 作为初学者理解 React 虚拟 DOM

> 原文：<https://javascript.plainenglish.io/understand-react-virtual-dom-as-a-beginner-d90b3935bce2?source=collection_archive---------9----------------------->

## 大家都在谈论它，你知道它是什么吗？

![](img/3143a878905975ab9fd941457c01720b.png)

Photo by author and [Julien](https://unsplash.com/photos/EWg1-0UjeWY) at [unsplash](https://unsplash.com)

**通过在**[**【https://twitter.com/antondevv】**](https://twitter.com/antondevv)**的 Twitter 上关注我，保持反应和打字的前沿。**

本文旨在教您一些关于 DOM 的知识，以及 React 虚拟 DOM 与它的不同之处，以及它们如何在高层次上进行交互。

## **首先，我们来澄清一些事情:**

HTML 是网页的标记(类似于结构)，JavaScript 用于与网页交互。

加载网站时,( HTML)文件会加载到浏览器中。JavaScript 不能直接理解 HTML 文档——它读起来像胡言乱语。这就是 DOM 的用武之地。DOM 只是 HTML 页面以面向对象方式的高级抽象。

那么什么是 DOM 呢？

它代表**文档对象模型**，是基于对象和节点的网站表示。基本上，它是一种面向对象的方法来描述网站，JavaScript 可以访问和操作那些属性。顺便说一下，如果你是一个前端开发人员，并且想了解一些关于 DOM 的事情，可以在这里查看我的文章[](/6-killer-facts-you-need-to-know-about-the-dom-as-a-frontend-developer-caf9872e4ae2)**。**

**无论如何，DOM 是一个 web API，它存在于 JavaScript 运行时中，这就是为什么我们可以访问 DOM 并与之交互，因为 DOM 根本不是 JavaScript 的一部分；它只是一个 web API，我们可以在某些 JavaScript 运行时访问它，这些运行时将 DOM 作为 web API 提供。**

**HTML 的元素成为 DOM 中的*节点*。记住，JavaScript 不能直接理解 HTML，所以它需要以面向对象的方式创建 HTML 的高级抽象。**

**所以作为 web API 的 DOM 允许我们使用 JavaScript 与之交互。例如，我们可以通过执行以下操作来更改一个**

# **标签:**

# **更新 DOM 时出错**

**那么为什么更新 DOM 甚至是一件坏事呢？**

**首先，这是一个烂摊子，它可以很快变得相当复杂。**

**此外，这可能是非常低效的。在 DOM 被绘制到屏幕上之前，浏览器需要包括解析、计算 CSS、布局等。所以，假设我们改变了 50 个 DOM 节点。浏览器需要为每个节点做所有这些，重新渲染会非常慢。**

**当状态改变时，浏览器需要找出需要重新呈现的内容。如果整个 DOM 需要重新渲染，或者只是部分需要重新渲染，等等。**

**一个例子是，如果我们每秒渲染一段 HTML，带有一个标题和一个每秒增加 1 的`count`,那么每秒，整个 DOM 将被更新，而不仅仅是计数。但是有了 React 和虚拟 DOM 的使用，DOM 中唯一会更新的是`count`,它将再次被绘制到屏幕上。因此，使用所谓的 diffing 算法，React 使得更新 DOM 更加有效。**

# **什么是虚拟 DOM？**

**这是官方 [**React 文档**](https://reactjs.org/docs/faq-internals.html) 关于它的说法:**

> **虚拟 DOM (VDOM)是一个编程概念，其中 UI 的理想或“虚拟”表示保存在内存中，并与“真实”DOM 同步**

**React 为 DOM 拥有的每个 DOM 对象提供一个虚拟 DOM 对象，它充当真实 DOM 对象的轻量级副本。这就是虚拟 DOM，它只不过是真实 DOM 的一个轻量级克隆。React 在幕后有算法可以在虚拟 DOM 的帮助下有效地更新真实 DOM，反之亦然，但是这是如何以及何时发生的呢？**

**当一个组件的状态改变时，整个虚拟 DOM 被更新；这看起来很不方便，但并不是因为虚拟 DOM 非常轻便和快速。这就像仅仅因为屏幕上什么也没画就更新一个对象。然而，当您的应用程序扩展并且您有许多相互依赖的组件时，重新渲染可能难以避免，并且实际上可能会降低性能，尤其是当您有一个组件重新渲染时触发的昂贵操作时。所以请记住:这种状态变化会导致一连串的重新渲染吗？它是好的还是需要一些关注？**

**然后将新的虚拟 DOM 对象与状态更新前的对象进行比较。React 然后确定哪些虚拟 DOM 对象已经被改变(这被称为 diffing)，并且一旦它确定了哪些虚拟 DOM 对象已经被改变，它就仅用那些已经被改变的新对象来更新真实 DOM，使用智能和高效的算法来用正确和必要的改变来更新 DOM。但是为什么它比你可能听说的要快呢？**

**因为当我们的 React 组件中发生状态变化时，我们的虚拟 DOM 首先被更新，然后它将它与之前的虚拟 DOM 进行比较，并且只更新那些需要更新的真实 DOM 的节点，并且它这样做是高效的。它还批量更改以提高效率。因此，它不会一次更新一个节点，而是将所有更改更新一次。**

**如果我们的 web 应用程序很大，并且我们使用简单的 JavaScript 来更新 DOM，这可能是一个昂贵的过程，因为 DOM 将不得不以低效的方式重新呈现，更不用说疯狂的复杂性了。**

## **结论:**

**对于 DOM 中的每个 DOM 对象，React 都有一个与之对应的“虚拟 DOM 对象”，就像它的一个轻量级副本。**

**因为 DOM 操作起来很慢，所以操作虚拟 DOM 更快，性能更好，而且最值得注意的是:有助于消除 DOM 的复杂性。**

# **如果你喜欢这件作品，我希望你也会喜欢:**

**[](/4-killer-ways-to-write-typescript-with-react-6a66b32764f1) [## 用 React 编写打字稿的 4 种黑仔方法

### 4 个黑仔打字稿，带反馈提示+ 1 个额外提示

javascript.plainenglish.io](/4-killer-ways-to-write-typescript-with-react-6a66b32764f1) [](/5-typescript-lessons-that-will-pay-off-911d35974c8) [## 将会有回报的 5 堂打字课

### 你知道第五条吗？

javascript.plainenglish.io](/5-typescript-lessons-that-will-pay-off-911d35974c8) [](https://betterprogramming.pub/callbacks-vs-promises-vs-async-await-a-step-by-step-guide-f93d13447604) [## 回调 vs .承诺 vs .异步 Await:逐步指南

### 引擎盖下也有点。

better 编程. pub](https://betterprogramming.pub/callbacks-vs-promises-vs-async-await-a-step-by-step-guide-f93d13447604) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***