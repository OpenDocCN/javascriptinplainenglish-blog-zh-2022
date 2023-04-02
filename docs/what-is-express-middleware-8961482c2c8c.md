# 什么是 Express 中间件？

> 原文：<https://javascript.plainenglish.io/what-is-express-middleware-8961482c2c8c?source=collection_archive---------7----------------------->

![](img/d26b236b25d8d724b2c160596ef2424f.png)

Photo by [Max Duzij](https://unsplash.com/@max_duz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你是一个网页开发者，那么你一定听说过 Express。Express 是 Node.js 的一个 web 框架，它使得创建 web 应用程序变得很容易。Express 最酷的特性之一是它对中间件的支持。在这篇博文中，我们将解释什么是中间件，以及如何使用它来改进开发过程。

## 中间件简介

那么，什么是中间件呢？中间件本质上是一段代码，在收到请求和返回响应之间执行。这允许您在应用程序逻辑运行之前修改传入的请求或执行某种操作。此外，中间件还可以用于在将输出响应发送回客户端之前对其进行修改。

## 为什么要使用中间件？

中间件提供了一种很好的方式来模块化您的代码，使其更具可重用性。此外，中间件可以用来执行不特定于任何一个路由或应用的任务。例如，您可以使用中间件来压缩响应体，然后再将其发送回客户端。这是提高应用程序性能的一个好方法。

使用中间件的另一个优点是，它可以用来为您的应用程序提供安全特性。例如，在允许用户访问敏感信息之前，您可以使用中间件来验证用户是否通过了身份验证。

## 如何使用中间件？

现在我们知道了什么是中间件以及为什么应该使用它，让我们来看看如何使用它。可以使用`use` 功能添加 Express 中间件。这个函数有两个参数:路径和中间件函数。path 参数指定将为其执行中间件功能的 URL。中间件函数是一个回调函数，它有三个参数:请求对象、响应对象和下一个函数。

下面是一个简单的例子，说明如何创建一个记录每个请求的 URL 的中间件:

```
function logURL(req, res, next) { console.log(req.url); next();}app.use(‘/’, logURL);
```

在这个例子中，我们使用`use`函数将我们的中间件函数添加到与`‘/’`匹配的 URL 的应用程序中。中间件函数只是将 URL 记录到控制台，然后调用`next`函数。这一点很重要，因为它告诉 Express 中间件功能已经完成，可以继续下一个中间件或应用程序逻辑了。

如果您希望您的中间件功能对所有 URL 都执行，那么您可以简单地省略 path 参数:

```
app.use(logURL);
```

这将导致对所有请求执行中间件功能。虽然这段代码将对所有的 URL 执行，但重要的是要注意中间件的顺序在您的代码中很重要。

![](img/c7ad2d2a4cd962c29f0e3a915a28d2ad.png)

Photo by [Green Chameleon](https://unsplash.com/@craftedbygc?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 中间件的顺序

值得注意的是，向应用程序添加中间件的顺序可能很重要。这是因为中间件的每一部分都是自顶向下执行的。例如，考虑以下代码:

```
app.use(logURL);app.use(‘/admin’, verifyUser);
```

在这段代码中，将为所有请求执行`logURL`中间件函数。然而，如果我们将我们的`app.use(logURL)`移到代码的最后一行，那么它将只为不匹配'/admin '的请求执行。这是因为`verifyUser`中间件函数会拦截所有对`/admin`的请求，并阻止`logURL`函数被调用。

## 错误处理中间件

一种特殊类型的中间件是错误处理中间件。这种类型的中间件用于处理应用程序中出现的错误。错误处理中间件有四个参数:错误对象、请求对象、响应对象和下一个函数。

下面是一个如何创建错误处理中间件功能的简单示例:

```
function errorHandler(err, req, res, next) { console.error(err); res.status(500).send(‘Something went wrong!’);}app.use(errorHandler);
```

在这个例子中，我们使用“use”函数将我们的错误处理中间件函数添加到应用程序中。如果我们的代码中出现错误，错误处理中间件功能将“捕捉”错误，并相应地处理它。这个中间件函数只是将错误记录到控制台，然后将响应的状态代码设置为 500，然后发回一条消息说“出错了！”。

## 学习 Express 中间件的其他资源

我们在本文中讨论的只是 Express 中间件的介绍。中间件非常强大，但是看起来很复杂。从本文中，您了解了关于 Express 中间件的基本概念。这通常有助于将这些概念可视化，因此我将链接一些帮助我学习 Express 中间件的视频。

*   [14 分钟学会 Express 中间件](https://www.youtube.com/watch?v=lY6icfhap2o&t=680s)
*   [中间件到底是什么东西](https://www.youtube.com/watch?v=MIr1oxQ3pao)

这些视频将有助于加深您对中间件的了解，并帮助您直观地了解中间件在生产中是如何使用的。

希望这篇文章教会你一些东西！祝你的编码项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*