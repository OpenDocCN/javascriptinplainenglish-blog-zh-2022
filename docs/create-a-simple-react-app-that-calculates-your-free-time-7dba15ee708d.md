# 创建一个 React 应用程序来计算你的空闲时间。

> 原文：<https://javascript.plainenglish.io/create-a-simple-react-app-that-calculates-your-free-time-7dba15ee708d?source=collection_archive---------12----------------------->

![](img/506820f5777bfe18c51b91e2078d953c.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇文章中，我将简要介绍一下 [React](https://reactjs.org) ，我们将构建一个简单的空闲时间计算器应用程序，就像 [**这个**](https://jtogofe-tmnt.netlify.app) **。**

首先，让我们大致了解一下我们今天要完成的任务。

# **概述**

1.  什么是反应？
2.  React 入门
3.  项目代码

# 什么是反应？

React 是 Meta(以前的脸书)开发的前端 JavaScript 框架，它使得创建 web 应用程序变得简单。

React 使用虚拟 DOM，这使得更新网页上的内容变得快速而简单，用户不需要刷新页面就可以看到更新。它给你的网站一种实时的感觉。

React **允许开发人员创建可以改变数据的大型 web 应用程序，而无需重新加载页面**。React 的主要目的是快速、可伸缩和简单。它只在应用程序的用户界面上起作用。这对应于 MVC 模板中的视图。

# React 入门

如前所述，React 是一个 JavaScript 框架，这意味着它需要一个可以运行 JavaScript 代码的环境。

通常，我们的计算机无法理解 JavaScript。这就是 Node.js 的用武之地。Node.js(或简称 Node)是一个 JavaScript 运行时环境，它使我们的计算机能够运行 JavaScript 代码。但是我们必须在 React 应用程序工作之前安装 Node。

要安装 Node.js，请访问他们的网站[并下载适用于您各自操作系统的 LTS 版本，然后运行安装程序。](https://nodejs.org/en/download/)

要确认安装，请打开终端(在 Linux / Mac 上)或命令提示符(在 Windows 上— WindowsKey + R，然后键入 cmd 并按 Enter)。您应该能够运行这些命令——当然，您的版本将与我的不同。

Check your Node JS version

现在剩下的就是创建我们的项目了。在您的终端中键入以下命令。

您的示例 React 应用程序应该位于 [http://localhost:3000](http://localhost:3000) 在您的浏览器中打开此 URL 并查看您的应用程序。

# 项目代码

现在，在您最喜欢的代码编辑器中打开您的项目，让我们开始编码。尝试更改 App.js 的内容，您会注意到什么？

当我们修改代码时，React 会自动更新我们的应用。这种行为类似于它根据应用程序状态或数据的变化来更新我们的应用程序。

此时，我们可以开始构建我们的应用程序了。首先，我们需要创建一个组件目录(又名文件夹),并在该文件夹中创建一个 index.js 文件，然后将这段代码粘贴到 components/index.js 文件中并保存它。

让我们检查一下刚刚添加的代码。我们简单地创建了两个组件

组合框(ComboBox)—一个预定义活动的列表，我们可以过滤这些活动以获得列表中的一个项目，或者根据需要随时添加到列表中。

**ActivityForm** —让我们添加日常活动的表单，并将它们存储在一个状态中。但是什么是国家呢？

状态是我们的应用程序运行所需的临时数据。我们的 React 应用程序监视状态的任何变化，并在 UI 中反映这些变化

我们还做了一些表单处理，以确保当用户单击表单上的“Add”按钮时，我们的数据被发送到我们的主应用程序进行处理。

现在，在 App.js 中粘贴这段代码来替换样板代码。

Your new App.js (or App.jsx)

我们刚刚做了什么？我们已经更新了 App.js 文件来呈现和处理组件发送的事件。我们还添加了数学逻辑，根据我们每天的活动数量来计算我们的空闲时间。

接下来，我们希望我们的应用程序有一个漂亮的外观和用户体验，所以让我们这样做。

在 App.css 中用这个替换内容，现在保存您的更改并检查您的浏览器。

哇！我们的应用程序看起来不错。让我们试一试。这样我们就可以知道我们一天有多少空闲时间。你可以在我的 [Github](https://github.com/ogofe/tmnt/) 上找到完整的应用代码

如果你喜欢这个演示，请跟随我上 [Github](https://github.com/ogofe) 开始回购。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***