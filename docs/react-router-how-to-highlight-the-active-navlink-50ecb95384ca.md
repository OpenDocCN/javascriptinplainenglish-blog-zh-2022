# React 路由器:如何突出显示活动导航链接

> 原文：<https://javascript.plainenglish.io/react-router-how-to-highlight-the-active-navlink-50ecb95384ca?source=collection_archive---------2----------------------->

![](img/57955eef479f6b058cf9524a59db4933.png)

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

导航是网站最重要的元素之一。它帮助人们找到他们想要的东西，并为他们浏览不同的页面提供了一个简单的方法。

当您使用 React Router 时，如果您突出显示活动导航链接，以便用户立即知道他们在哪个页面上，这可能会很有帮助。这样做也有助于他们理解页面是如何组织的，让他们更容易浏览你的网站。

## NavLink 组件

在 React Router 中，您可以使用 NavLink 组件突出显示活动的导航链接。这个组件用来在你的导航栏中创建一个链接，并且有几个属性可以用来设置链接的样式。突出显示导航链接时最重要的属性是 activeClassName 和 activeStyle 属性。

## activeClassName 属性

activeClassName 属性接受一个字符串，并在活动时将指定的类名添加到链接中。您可以使用此属性创建一个样式，该样式将在 NavLink 处于活动状态时应用。例如，我们可以将一个选定的类添加到活动链接中。

```
<NavLink to="/" activeClassName="selected">Home</NavLink>
```

## activeStyle 道具

activeStyle 属性接受一个对象，并在链接处于活动状态时将指定的样式应用于链接。如果您想要应用与类无关的样式，这可能会很有用。例如，我们可以将活动链接的颜色设置为蓝色。

```
<NavLink to="/" activeStyle={{ color: "blue" }}>Home</NavLink>
```

## 结论

突出显示导航栏中的活动链接是一种很好的方式，可以帮助用户了解他们所在的页面，并使他们更容易浏览您的网站。当您使用 React Router 时，可以通过设置 activeClassName 和 activeStyle 属性，使用 NavLink 组件轻松突出显示活动链接。使用这些属性，您可以创建自定义样式，当链接处于活动状态时，这些样式将应用于链接。希望这篇文章教会你一些东西！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***