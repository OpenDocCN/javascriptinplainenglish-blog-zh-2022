# 如何使用 Webpack 设置多个环境

> 原文：<https://javascript.plainenglish.io/how-to-set-up-multiple-environments-with-webpack-90082c3b28ea?source=collection_archive---------6----------------------->

![](img/44ad31cd3b13e034092a2fcdab0ba424.png)

用 Webpack 设置多个环境是每个人都应该利用的一个重要特性。

就 Webpack 提供的粒度级别而言，很难找到您确切需要的说明。

在本文中，我将展示如何配置我的环境。我的例子包括实现环境，而不是通常的开发和生产环境。

我将给出 4 个环境的例子:本地、Cypress、开发、生产。我的确认位于 webpack.config.js 文件中。

首先，我创建一个公共对象，其中包含所有环境使用的任何配置:

之后，我为我想要支持的每个环境添加了一个新的 Webpack 配置对象。使用 spread 运算符，我可以轻松地包含 common 中的所有值:

现在我可以定制这些对象来支持我所需要的。

在我的例子中，本地和 cypress 环境都运行 webpack-dev-server，但是 cypress 不需要本地的所有配置。类似地，我的开发和生产环境使用不同的 index.html 文件，这个配置允许我适应它。

一旦我的对象配置好了，我需要在文件的末尾添加一个 return 语句。

以下是完整的文件示例:

最后一步是当我从脚本中调用某个命令时设置 NODE_ENV:

在大多数示例中，NODE_ENV 被设置为开发或生产，但是没有什么可以阻止您将其设置为您想要的任何值。

希望我的例子能给你一些关于如何设置你自己的 Webpack 配置的想法。我敢肯定，你甚至可以用我的方法来重构它，使它更加有效。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*