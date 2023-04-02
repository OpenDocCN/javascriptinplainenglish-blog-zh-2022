# React 路由器 NavLink、Link 和的区别

> 原文：<https://javascript.plainenglish.io/react-router-dom-the-differences-between-navlink-link-and-a-bb5c27a48bfc?source=collection_archive---------3----------------------->

## 如何使用 NavLink、Link 和——举例说明。

![](img/f3ed982614df562f914b5973c7172524.png)

Photo by [Scott Graham](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当使用 react-router-dom 时，有三种主要的方法来创建链接:NavLink、Link 和 anchor 标签(`<a>`)。在本文中，我们将解释这三种方法之间的区别。我们也将提供如何使用每一个的例子。我们开始吧！

## 环

链接组件由 react-router-dom 提供，用于在应用程序中导航。它在引擎罩下呈现一个锚标记(`<a>`)，链接到内部路由。链接组件利用“to”属性，该属性可以是字符串或对象。如果“to”属性是一个字符串，它将呈现一个锚标记，其`href` 等于该字符串。

如果“to”属性是一个对象，它将呈现一个锚标记，其`href` 等于该对象的路径名。如果使用“to”属性的对象版本，您可以传递四个不同的属性:pathname(路径链接)、search(查询参数)、hash(放入 URL)和 state(持久状态)。

示例:

## NavLink

NavLink 是 react-router-dom 提供的一个组件，它允许用户在整个 react 应用程序中导航。NavLink 类似于 Link，但是它能够向元素添加额外的样式属性。例如，您可以使用 NavLink 以不同于其他链接的方式设置活动链接的样式。NavLink 利用“activeClassName”属性。这是当元素处于活动状态时将应用于该元素的类。

示例:

NavLink 组件的 activeClassName 为“active ”,它将在用户位于“关于”页面时启用。您可以在 CSS 文件中设置 activeClassName 的样式。例如，如果我们希望 NavLink 处于活动状态时为绿色，我们可以编写以下 CSS:

![](img/852f1970a7d2c48190d423c7c6c2e9e6.png)

Photo by [Thanzi Thanzeer](https://unsplash.com/@thanzi7?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 锚标记()

锚定标签是一个 HTML 元素，用于创建到另一个页面的链接。锚标记有一个`href` 属性，它指定链接所指向的页面的 URL。锚标记不同于 Link 和 NavLink，因为它不使用 React 路由器。它用于链接到外部页面，或者用于在 React 应用程序中创建不指向特定路径的链接。

示例:

## 什么时候用哪个？

现在我们已经讨论了每个链接的不同之处，您应该在什么时候使用哪个链接呢？如果您想在 React 应用程序中创建一个链接，当它处于活动状态时不需要样式，请使用 link 组件。如果您想在 React 应用程序中创建一个链接，当它处于活动状态时确实需要样式，请使用 NavLink 组件。最后，如果您想在 React 应用程序中创建一个指向外部页面或非路由的链接，请使用 anchor 标记。

## 结论

总之，在使用 React Router DOM 时，有三种方法可以创建链接:NavLink、Link 和 anchor 标记(`<a>`)。我们讨论了每个链接之间的差异以及何时应该使用每个链接。现在您已经知道了它们的区别，您可以在 React 应用程序中相应地利用每个链接。

我希望这篇文章能教会你一些东西。祝你的项目好运！

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*