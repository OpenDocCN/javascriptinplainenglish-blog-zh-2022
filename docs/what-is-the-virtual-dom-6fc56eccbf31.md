# 什么是虚拟 DOM？

> 原文：<https://javascript.plainenglish.io/what-is-the-virtual-dom-6fc56eccbf31?source=collection_archive---------7----------------------->

## 解释什么是虚拟 DOM 以及虚拟 DOM 是如何工作的。

![](img/7199c977e881611f69d9550a7db79e2d.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您是 web 开发人员，那么您可能听说过虚拟 DOM。但是到底是什么呢？在本文中，我们将解释 ccccc，我们还将讨论在您的项目中使用虚拟 DOM 的一些好处。

## 虚拟 DOM 简介

虚拟 DOM 是 DOM(文档对象模型)的虚拟表示。虚拟 DOM 可以被认为是实际 DOM 的蓝图。它是一个 JavaScript 对象，包含与 DOM 相同的信息。

虚拟 DOM 包含构建真实 DOM 所需的所有信息，并且它具有与实际 DOM 对象相同的属性。然而，虚拟 DOM 不能直接修改屏幕上显示的内容。

## 虚拟 DOM 的优势

引入虚拟 DOM 是为了帮助提高 web 应用程序的性能。当使用虚拟 DOM 时，浏览器不必在每次有变化时都重新呈现整个页面。

相反，仅更新已更改的元素。当发生更改时，虚拟 DOM 将更新更改的元素，然后尝试将更改与实际 DOM“同步”。将虚拟 DOM 与真实 DOM 进行比较可以显著提高性能，因为应用程序只需更新已更改的元素。

![](img/4bfef1c107ad398aa7d6f2db6e0faae7.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 更新 DOM 的步骤

既然我们已经讨论了什么是虚拟 DOM，那么让我们来分解更新 DOM 所涉及的步骤。

1.  应用程序将对数据模型进行更改。这可以响应于用户输入来完成，或者可以是由应用程序自动做出的改变。
2.  虚拟 DOM 将会更新，以反映对数据模型所做的更改。
3.  虚拟 DOM 中已更改的元素将与实际 DOM 中的相应元素进行比较。
4.  更改后的元素将在实际的 DOM 中更新，浏览器将相应地重新呈现页面。

## 结论

虚拟 DOM 是一个强大的工具，可以帮助提高 web 应用程序的性能。通过利用虚拟 DOM，您可以对数据模型进行更改，而不必重新呈现整个页面。

我希望这篇文章消除了您对虚拟 DOM 的任何困惑。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***