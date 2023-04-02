# 你不需要 React 来创建一个可重用的按钮！

> 原文：<https://javascript.plainenglish.io/you-dont-need-react-to-create-a-reusable-button-2108cfeac38c?source=collection_archive---------4----------------------->

## 请改用 Web 组件！

![](img/3208340cbcd4ce39b0167b94f5e7da07.png)

Photo by [Donald Giannatti](https://unsplash.com/@wizwow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

假设你是自愿阅读这篇文章的，那么很有可能你已经使用了一些**材料设计框架**。有很多:Angular 的 Angular Material，VueJs 的 Vuetify，React 的 Material UI 等等。一个可能比另一个好一点。尽管如此，它们主要提供相同的可重用 UI 组件，如按钮、输入、对话框等。通过让前端组件在整个框架中发挥作用，在一个统一的 web 中共享它们不是很好吗？

在这篇文章中，我将向您展示 **Web 组件**如何通过用一个本地的统一解决方案替换 Web 应用程序的组件层来简化和改进万维网。拥有基于官方 web 标准的可互换、可重用的前端组件可以大大降低前端框架之间的转换成本。这样，如果公司从一开始就依赖于组件库的统一和标准化的解决方案，他们可以节省大量的资金。

[](https://medium.com/@mariusbongarts11/will-web-components-replace-frontend-frameworks-535891d779ba) [## Web 组件会取代前端框架吗？

### 它们是为解决不同的问题而构建的。

medium.com](https://medium.com/@mariusbongarts11/will-web-components-replace-frontend-frameworks-535891d779ba) 

# 什么是 Web 组件？

Web 组件是基于官方 web 标准的可重用客户端组件，受所有主流浏览器支持。它们是将**功能从其余代码中封装出来的一种极好的方式。不仅如此，你还可以在每个网络应用程序和网页中重用它们。**

> *Web 组件的主要好处是我们可以在任何地方使用它们。有任何框架，甚至没有框架。——*[*vuejs.org*](https://v3.vuejs.org/guide/web-components.html)

## 它们是如何工作的？

下面是一个如何定义**自治 web 组件**的例子:

```
class MyWebComponent extends HTMLElement {...}window.customElements.define('my-button', MyWebComponent);
```

您可以将元素传递给任何 HTML 页面，如下所示:

`<my-button value="something"></my-button>`

如果你想玩玩 Web 组件，这里有一个 Hello World starter[CodePen](https://codepen.io/marius2502/embed/YzQVazx?)。有关 web 组件的更多详细信息，请查看我的其他文章:

[](https://medium.com/@mariusbongarts11/the-complete-web-component-guide-part-1-custom-elements-a627af805df8) [## 完整的 Web 组件指南:自定义元素

### 成为 Web 开发未来的专家(第 1 部分)

medium.com](https://medium.com/@mariusbongarts11/the-complete-web-component-guide-part-1-custom-elements-a627af805df8) [](https://medium.com/@mariusbongarts11/showcase-your-medium-articles-with-web-components-part-1-basics-d2c6618e9482) [## 用 Web 组件构建自己的博客组合:基础

### 第 1 部分—定制元素、阴影 DOM 和 HTML 模板

medium.com](https://medium.com/@mariusbongarts11/showcase-your-medium-articles-with-web-components-part-1-basics-d2c6618e9482) 

# 供应商锁定的成本

为了理解为什么转换到组件库的标准化解决方案可以节省时间和金钱，我们需要理解**供应商锁定**的问题。

**假设一家公司使用 React 开发了一个高度复杂的 web 应用程序。数百名开发人员正全职从事这项工作。他们创建了自己的内部 React 组件库。这有助于[最小化系统内的代码重复](https://medium.com/@mariusbongarts11/dry-your-wet-typescript-code-e3c777b3daf9)，这非常好！**

**众所周知，软件行业是发展最快、变化最大的行业之一。这伴随着软件工程的许多变化和创新。假设，明年，有人将发布最终的前端框架，这将盖过任何现有的框架。**

**越来越多的开发人员正在采用新的框架。随着时间的推移，公司将在新项目中使用该框架，一些公司将迁移现有的项目。React 将不再高效，寻找优秀的 React 开发人员变得越来越复杂和昂贵。**

> **供应商锁定是指某人被迫继续使用某种产品或服务，而不管其质量如何—[cloudflare.com](https://www.cloudflare.com/learning/cloud/what-is-vendor-lock-in)**

**我们例子中的公司将**锁定**到下级前端库 React。转换到新框架将非常昂贵，并且可能会中断业务运营。应用程序的每个前端组件都必须迁移到新的框架中。更糟糕的是，每个使用这些组件的应用程序都需要改变其按钮、链接、对话框等的集成。**

> **作为开发人员，您可以自由地在您的 Web 组件中使用 React，或者在 React 中使用 Web 组件，或者两者都使用。—[reactjs.org](https://reactjs.org/docs/web-components.html)**

**我希望大家越来越清楚，使用 **Web 组件**可以为我们公司节省很多钱。甚至 React 本身也建议在其官方文档中使用 Web 组件:**

> **大多数使用 React 的人不使用 Web 组件，但是您可能想使用，尤其是如果您使用的是使用 Web 组件编写的第三方 UI 组件。—[reactjs.org](https://reactjs.org/docs/web-components.html)**

# **Web 组件的组件库**

**设计一个组件库不是一件容易的事情。它需要一长串的决定，这些决定可能会变得令人难以招架。幸运的是，我们不需要从头开始。已经有一些由公司维护的 Web 组件库，例如 Google 和 SAP:**

*   **[**Material Web Components(MWC):**](https://github.com/material-components/material-web)遵循 Google 材料设计原则的 Web 组件集合。**
*   **[**聚合物元素:**](https://github.com/PolymerElements?page=3) 谷歌的聚合物库可以让你构建封装的、可重用的 Web 组件，就像标准的 HTML 元素一样工作**
*   **[**Vaadin Web 组件:**](https://github.com/vaadin/vaadin) Vaadin 组件是一组不断发展的高质量用户界面 Web 组件**
*   **[**openui 5**](https://github.com/SAP/ui5-webcomponents)**:**SAP 丰富的企业级可重用 UI 元素，由轻量级框架驱动**

**可惜我觉得那些组件还没有比如 React 的 Material UI 那么成熟。但是，开发者对此贡献越多，它就会变得越好。**

# **最后的想法**

**使用 Web 组件作为组件库的基础为各种可预测和不可预测的用例提供了合适的解决方案。Web 标准使我们的前端应用程序更能容忍变化，并能防止公司受到供应商的束缚。那可以省很多钱。**

**我想强调的是，我并不是建议用 Web 组件完全取代前端框架。我在以前的一篇文章中详细讨论过这个问题，[Web 组件会取代前端框架吗](https://medium.com/@mariusbongarts11/will-web-components-replace-frontend-frameworks-535891d779ba)？。我认为它们不会很快取代前端框架。然而，他们可以通过用本地的统一解决方案替换组件层来增强这些框架。**

**我希望你喜欢阅读这篇文章。你对 Web 组件有什么看法？欢迎发表评论。我总是很乐意回答问题，也乐于接受批评。随时联系我😊**

**这里是无限制访问媒体上所有内容的链接。如果你用这个链接注册，我会赚一小笔钱，不需要你额外付费。**

**[](https://medium.com/@mariusbongarts/membership) [## 通过我的推荐链接加入 Medium-Marius bong arts

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@mariusbongarts/membership) 

关注我，不要错过我的下一篇文章。我写了关于 Typescript、Web 组件、前端框架、软件设计模式、Chrome 扩展以及更多的主题！🙏

# 关于作者

Marius Bongarts 是埃森哲互动公司的软件工程分析师。他还创建了 [Web Highlights Chrome 扩展](https://chrome.google.com/webstore/detail/web-highlights-%20-bookmark/hldjnlbobkdkghfidgoecgmklcemanhm)，允许成千上万的用户在每个网站上创建文本亮点和书签。通过提供标签和目录，您可以在 web-highlights.com 的[上的相应网络应用程序中轻松重新找到您的网络研究。看看吧！](https://web-highlights.com/home)

通过**[**LinkedIn**](https://www.linkedin.com/in/marius-bongarts-6b3638171/)**联系我或者在 [**Twitter**](https://twitter.com/MariusBongarts) 上关注我。****

****[](https://medium.com/@mariusbongarts11/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [## 我的第一个 9.99 美元之旅与我的副业

### Chrome 扩展带来的被动收入

medium.com](https://medium.com/@mariusbongarts11/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [](https://medium.com/@mariusbongarts11/react-vs-web-components-80d754f74811) [## React 与 Web 组件

### 将它们结合起来是成功的真正秘诀。

medium.com](https://medium.com/@mariusbongarts11/react-vs-web-components-80d754f74811) 

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。********