# React 路由器:如何使用 useParams()钩子

> 原文：<https://javascript.plainenglish.io/react-router-how-to-use-the-useparams-hook-321a6461732?source=collection_archive---------1----------------------->

## 关于如何使用 useParams()钩子来改进 web 应用程序的指南(带有示例)。

![](img/fd95f7f2d8d88d35176bc3a1855b5ab6.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/es/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个用于构建用户界面的流行 JavaScript 库。React 最棒的一点是，它允许您使用钩子向组件添加功能。在本文中，我们将讨论如何在 React 中使用`useParams()`钩子。我们还将提供一些例子，说明如何使用这个钩子来改进 web 应用程序。

## useParams()简介

`useParams()`挂钩是一个 React 路由器挂钩，允许您访问当前 URL 的参数。如果您希望基于 URL 参数动态呈现内容，这可能会很有用。例如，如果您有一个博客应用程序，您可能希望根据 URL 中的文章 ID 呈现不同的文章。

## 反应路由器

React Router 提供了许多其他挂钩，您可以使用它们向 React 组件添加功能。`useParams()`钩子来自 react-router 包。要使用这个钩子，您需要在您的项目中安装 React 路由器。

为了安装 React 路由器，您需要使用一个包管理器，如 npm 或 yarn。React Router 有很棒的文档和教程，关于如何开始。你可以在这里访问设置 React 路由器[的教程。](https://reactrouter.com/)

![](img/2d4c8b26aa7feb219e4e52234cb13fd7.png)

Photo by [Safar Safarov](https://unsplash.com/@safarslife?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 利用 useParams()

一旦在项目中安装了 React Router，就可以从 react-router 包中访问`useParams()`钩子。您可以将这个挂钩导入到您的组件中，如下所示:

```
import { useParams } from ‘react-router’;
```

`useParams()`钩子返回一个包含当前 URL 参数的对象。例如，如果您有这样一条路线:

```
<Route path=”/articles/:articleId” />
```

网址是:

```
/articles/123
```

`useParams()`钩子将返回一个键为`articleId` 值为 123 的对象。您可以通过析构由`useParams()`返回的对象来访问 URL 参数的值。例如:

```
const { articleId } = useParams();console.log(articleId); // 123
```

然后，您可以使用`articleId`参数来动态呈现组件中的内容。

## 结论

在本文中，我们讨论了如何在 React 中使用`useParams()`钩子。我们还提供了一个例子，说明如何使用这个钩子来改进 web 应用程序。我希望这篇文章能教会你一些东西。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***