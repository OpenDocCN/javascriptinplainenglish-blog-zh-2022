# Node.js 开发人员必须知道的 5 个 npm 包

> 原文：<https://javascript.plainenglish.io/5-must-know-npm-packages-for-node-js-developers-a813068aeb8b?source=collection_archive---------15----------------------->

## Node.js 开发人员必须知道的一些基本 npm 包

![](img/ccc29c1c2ea1815ed7ececdb84b1735c.png)

Photo by [Brandable Box](https://unsplash.com/@brandablebox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本教程中，我们将介绍一些 Node.js 开发人员在进行 Node.js 开发时必须知道或可能遇到的基本 npm 包。

如果您是 Node.js 开发人员的初学者，一般的入门知识将帮助您熟悉为什么以及何时使用某些包。

但在此之前，***node . js 到底是什么？***

大多数人的一个误解是 Node.js 是一种后端编程语言。是吗？答案很简单，不是。

那么，到底为什么要用 Node.js 呢？

Node.js 是一个运行时引擎，构建在 Chrome 的 V8 JavaScript 引擎之上，有助于在除浏览器之外的任何地方运行 JavaScript。它编译 JavaScript 代码，并将其翻译成机器可读的代码。

简而言之，就像 Chrome 的 js 引擎提供了在浏览器上运行 JavaScript 代码的能力一样，Node.js 提供了在服务器上运行 JS 代码的能力。

好了，现在一旦清楚了这一点，让我们继续这个主题的主要议程，让我们探讨 5 个重要的 npm 包。

1.  [Express](https://www.npmjs.com/package/express) :这是一个基于 Node.js 开发的框架，用于以更简单的方式开发基于 Node.js 的应用程序。Express 提供了几个内置的特性，比如路由器，这反过来有助于更快速和无缝的开发。每周下载量在 24，222，272 之间，目前 Express 和 Node.js 是最受欢迎的合作伙伴之一，尽管还有一些其他框架也同样受欢迎，比如 Koa.js、NestJS 等等。
2.  [CORS](https://www.npmjs.com/package/cors) :每当客户端和服务器之间有通信时，你一定会在浏览器中看到一个可怕的错误，即
    “***对 XMLHttpRequest 的访问被 CORS 策略***”
    当客户端和服务器应用程序驻留在不同的端口上并试图通信时，就会出现这个错误。
    默认情况下，浏览器将这种通信视为不安全的，因此试图对其进行限制。
    这个问题的解决方案是在客户端和服务器端口之间需要有一个握手，而这正是 CORS 所提供的。
    有很多配置，可以在服务器端添加，让通信更安全。
3.  b[body-parser](https://www.npmjs.com/package/body-parser):从客户端发送的请求正文必须经过验证，然后才能在服务器端的任何地方使用，为此，它们必须通过中间件，即 body-Parser。
    本验证请求之前. body 不能使用。它们帮助解析 JSON、原始、文本和 URL 编码的请求正文。
    ***只是一个旁注*** :在较新版本的 Express 中，他们有自己的 body-parser 实现。因此，您可能不需要在较高的 Express 版本中单独安装该软件包，但知道这一点仍然很好。
4.  [Multer](https://www.npmjs.com/package/multer) :您一定注意到了，body-parser 验证各种请求，但不验证多部分/表单数据，即包含 blobs、图像、文件或任何复杂请求的请求。因此，为了满足这种要求，使用了 Multer。它提供了各种配置，如将文件/图像保存在文件夹中、重命名文件等。
5.  [插座](https://www.npmjs.com/package/socket.io)。 [io](https://www.npmjs.com/package/socket.io) :默认情况下，Node.js 为请求触发的单向数据流提供服务。然而，为了实现实时特性，需要在客户机和服务器之间保持双工或双向通信，socket.io 提供了同样的功能。
    socket . io 的好处是它也提供了一个兼容的前端库，即 socket.io-client，这有助于客户机和服务器之间的快速集成。

简而言之，这些是在 Node.js 开发过程中经常使用的几个包，你也可以把它们添加到你的工具包中，即使直到现在。
回复时，请告知我可添加到试剂盒中的其他包装。

但是在结束之前，让我再给你一个奖金方案，从实现的角度来看，这个方案并不那么重要，但是在进行开发的时候，这个方案非常重要。

*   [Nodemon](https://www.npmjs.com/package/nodemon) :该包作为开发依赖项添加到 package.json 中，因为它主要用于进行开发。很多时候，每当我们对文件进行更改时，我们都必须停止启动我们的 Node.js 服务器。Nodemon 提供了一个实时重新加载功能，即一旦任何更改保存在文件中，它就会自动重新加载服务器，我们不必一次又一次地停止和启动服务器。

所以，到此为止。
如果您希望我在回复中写些什么，请告诉我您的反馈、建议或话题。

你可以在这里阅读我的其他文章[，另外，你可以订阅我的时事通讯，获取我发表的最新文章。](https://medium.com/@avinash.dev21987)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****