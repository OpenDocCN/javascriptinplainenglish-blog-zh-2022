# Next.js 中的 3 种呈现类型

> 原文：<https://javascript.plainenglish.io/the-three-types-of-rendering-in-next-js-bd6f780270ac?source=collection_archive---------3----------------------->

## 它们是什么以及何时使用它们

![](img/1f3ddd1262cb0a926db38f04be782bf1.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Next.js 的好处之一是它在如何在用户浏览器上构建页面方面的多功能性。内容呈现的速度取决于应用程序的大小和类型。Next.js 有三个选项可供选择，以便页面以最佳速度呈现。

## 1.客户端渲染

这种非常常见的呈现形式依赖于用户的浏览器来构建页面。用 JavaScript 构建的应用程序，包括 React，通过它们的程序逻辑创建 HTML。当用户请求一个页面时，服务器响应并发送回一个空的 HTML shell 和 JavaScript 代码，然后页面所需的其余 HTML 基于 JS 代码构建在浏览器中。

这种方法非常适合构建单页面应用程序，因为只在给定时间按需生成所需的 HTML。一旦加载了 JavaScript 并且构建了页面的初始部分，它们会非常快。这样做的缺点是，根据 JavaScript 代码和 API 调用的复杂性，页面加载在开始时可能会很慢。这也可能对搜索引擎优化产生负面影响，因为他们可能需要更长的时间来接收页面信息。

## **2。服务器端渲染**

此方法涉及由服务器呈现的页面。对服务器的每个请求都会生成 HTML，这意味着它会向客户端提供一个完整构建的页面。服务器端呈现有利于在页面到达用户浏览器时提供完整的内容体验。搜索引擎优化也很好，因为搜索可以从已经构建的 HTML 中获得所需的数据，而不是等待 JavaScript 来呈现它。

服务器端呈现非常适合基本保持不变的页面。他们不能很好地处理内容不断更新的页面(比如股票信息、新闻和天气)或者需要频繁改变页面的应用程序。因为所有的 HTML 都是基于每个请求构建的，所以频繁的页面更改会影响性能。包含大量数据的页面也会导致问题，因为在请求页面和页面出现在浏览器上时会有明显的延迟。成本也是一个因素，因为需要更快的服务器来提供更好的性能。

## **3。静态生成**

Next.js 中呈现的第三个选项是最常用的。静态生成也在服务器端构建 HTML，但它不是在每个请求上呈现，而是在构建时呈现静态 HTML。然后在每个请求中重用呈现的 HTML。性能通常优于服务器端呈现，因为不需要在每次请求时都完全重建整个页面，因此在大多数情况下都推荐这样做。API 调用可以包含在页面的构建中以获取数据。搜索引擎优化也很好，因为 HTML 仍然在服务器端生成。

尽管尽可能使用静态生成是最好的，但它也有缺点。首先，如果 Next.js 应用程序有很多页面，构建时间会很长。更多的页面意味着需要生成更多的 HTML，更大的应用程序会对构建时间产生负面影响。另一个问题涉及不断更新新信息(股票、新闻和天气)的页面。API 调用是在构建时在服务器端完成的，因此那时检索的数据有过期的风险。顾名思义，静态生成最适合静态内容。

## **混搭**

Next.js 最棒的一点是，这三种呈现方法可以逐页使用，也可以相互结合使用，以便在任何情况下都能获得最佳性能。静态生成是大多数情况下的首选方法。然而，如前所述，如果应用程序有许多包含大量数据的页面，该怎么办呢？为了避免长的构建时间，服务器端呈现可能是一个更好的选择，因为它会在每次请求时加载 HTML 并提供更好的性能。

一些页面可能需要不断更新的数据。静态生成对于这一点并不理想，但是对于 Next.js 呈现，方法可以一起使用以获得最佳结果。页面的常规内容可以通过静态生成来构建，交付给用户的浏览器，这样他们就有了一个可查看的页面，然后可以使用客户端呈现来获取和加载动态内容。一个页面可以同时使用静态生成和客户端呈现来处理频繁的更新，而应用程序中不需要定期更新的其他页面可以只使用静态生成。根据页面和/或应用程序，混合搭配以实现最佳性能。

## **结论**

Next.js 中可用的渲染方法使其在性能上具有多功能性，这是单独使用 React 所无法实现的。了解每种方法的工作原理以及何时使用它们有助于创建完全优化且响应迅速的用户体验。因此，请了解每一个并释放 Next.js 的全部潜力！

*更多内容看* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*

**延伸阅读:**

[](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) [## 如何建立一个可组合的博客

### 从头开始创建一个博客需要很多。有许多移动的部件组合在一起形成一个…

比特云](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) [](https://bit.cloud/blog/extendable-uis-how-to-build-better-uis-for-developers-l1jkl1pc) [## 可扩展的 UI 组件

### 我最近受命为 bit.cloud 平台构建一个用户卡组件。我还负责建造…

比特云](https://bit.cloud/blog/extendable-uis-how-to-build-better-uis-for-developers-l1jkl1pc)