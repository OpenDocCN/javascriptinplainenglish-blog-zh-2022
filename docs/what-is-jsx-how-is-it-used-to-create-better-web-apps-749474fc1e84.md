# 什么是 JSX &如何使用它来创建更好的 Web 应用程序？

> 原文：<https://javascript.plainenglish.io/what-is-jsx-how-is-it-used-to-create-better-web-apps-749474fc1e84?source=collection_archive---------12----------------------->

## JSX 是一个 JavaScript 语法扩展，允许你直接在你的 JavaScript 代码中写 HTML 标签。

![](img/b8213deb8ae4d08eac7829622cec6d42.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JSX 是一个 JavaScript 语法扩展，允许你直接在你的 JavaScript 代码中写 HTML 标签。它是由脸书创建的，目的是使它的 ReactJS 库更加用户友好。JSX 帮助创建可重用的 UI 组件，这是 ReactJS 如此受欢迎的主要原因之一。在本文中，我们将讨论什么是 JSX，以及如何使用它来创建更好的 web 应用程序！

## 介绍 JSX

JSX 代表 JavaScript XML。JSX 允许你在 JavaScript 代码中嵌入 HTML 标签。JSX 将 HTML 标签转换成 JavaScript 代码，允许开发者将 HTML 标签直接嵌入到他们的 JavaScript 代码中。

## JSX 的动机

创建 JSX 是为了让 React 更加用户友好。当您使用 JSX 创建一个 React 元素时，您实际上是在创建一个创建 HTML 标签的 JavaScript 函数。这使得创建可重用的 UI 组件变得容易。此外，JSX 使得在你的 HTML 标签中嵌入表达式变得容易。这使得创建无需刷新整个页面即可更新数据的动态 web 应用程序成为可能。

JSX 允许将呈现逻辑嵌入到标记中，使得创建复杂的用户界面变得容易。利用 JSX，开发人员可以将 JavaScript 的强大功能与 HTML 的声明性结合起来，创建健壮的 web 应用程序。

JSX 还通过防止跨站点脚本(XSS)攻击来提高 web 应用程序的安全性。通过将 JSX 转换成 JavaScript，任何嵌入在 JSX 中的 HTML 都将在呈现之前被转义。这可以防止恶意用户输入作为代码执行，使您的 web 应用程序更加安全。

![](img/8b89323a36759c4dbe807d1ba35adbcb.png)

Photo by [Headway](https://unsplash.com/@headwayio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 使用 JSX 创建反应元素

JSX 使创建反应元素变得容易。React 元素是 React 应用程序的构建块。通过使用 JSX，您可以创建代表 React 元素的标签。例如，下面的代码使用 JSX 创建一个虚拟 DOM 节点:

```
const helloWorldNode = <h1> Hello World! </h1>;
```

helloWorldNode 变量是一个 React 元素。当这段代码被编译时，helloWorldNode 变量将被转换成一个创建 h1 标签的 JavaScript 函数。

## 在 JSX 嵌入表达式

您可以通过将表达式括在花括号中，在 JSX 中嵌入表达式。例如，以下代码在 JSX 标签中嵌入了一个 JavaScript 表达式:

```
const name = ‘John Doe’;const greetingNode = <h1> Hello, {name} </h1>;
```

greetingNode 变量将被传送到一个创建 h1 标记的 JavaScript 函数中。name 变量将被插入到 h1 标记中，创建一个可以随 name 变量变化的动态问候语。

## 结论

JSX 允许开发人员通过在 JavaScript 代码中嵌入 HTML 标签来构建动态 web 应用程序。利用 JSX 有很多好处，包括提高安全性和更容易创建可重用的 UI 组件。JSX 是 React 的关键组件，它彻底改变了 web 应用程序的开发方式。

我希望这篇文章能消除你的任何困惑！祝你的编码项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***