# Express 中路由的基础知识

> 原文：<https://javascript.plainenglish.io/the-basics-of-routing-in-express-d76bb28f8ab8?source=collection_archive---------12----------------------->

## 了解 Express 中路由的基本知识，以及如何为自己的应用程序创建路由。

![](img/8c36583e32b2b385a82d34c589c14901.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Express 是一个流行的 Node.js web 框架，提供路由功能。路由允许您将特定的 URL 映射到特定的处理程序，然后这些处理程序可用于处理请求和生成响应。在这篇博文中，我们将讨论 Express 中路由的基础知识，并向您展示如何为您自己的应用程序创建路由。

## Express 中的路由简介

在 Express 中，使用 HTTP 方法在您声明的 Express app 对象上定义路由。例如，要创建一个响应 GET 请求的路由，您可以使用 `app.get()`方法，对于 POST 请求，您可以使用`app.post()`。

这些方法有两个参数:一个路径和一个处理函数。path 是您希望映射到处理程序的 URL，而 handler 函数是当向该 URL 发出请求时将被调用的函数。

## 路由方法

正如我们上面提到的，有不同的方法对应于您可以处理的不同类型的请求。在 Express 中，这些方法是:

*   `app.get()` —用于处理获取请求
*   `app.post()` —用于处理发布请求
*   `app.put()` —用于处理 PUT 请求
*   `app.delete()` —用于处理删除请求
*   `app.patch()` —用于处理补丁请求

您还可以使用`app.all()`方法将任何类型的请求映射到一个处理函数。下面是为 GET 和 POST 请求定义的两个简单路由。

```
const express = require(‘express’)const app = express() // Handling GET requestsapp.get(‘/’, (req, res) => { res.send(‘Hello, world!’)}) // Handling POST requestsapp.post(‘/’, (req, res) => { res.send(‘Received a POST request’)})
```

在上面的代码中，我们首先需要 Express 模块，然后创建一个 Express 应用程序的实例。然后，我们可以使用上述方法定义我们的路线。接受两个参数 req 和 res 的回调函数是一个路由处理函数。我们将在后面的章节中更详细地讨论路由处理程序。

在第一条路线中，我们将根 URL `‘/’`映射到一个处理函数，该函数发送 Hello World 的简单消息作为响应。在第二条路线中，我们将同一个 URL 映射到一个不同的处理器函数，该函数也发送一条消息，但是这次它说我们收到了一个 POST 请求。

![](img/3a898fe88a569fa30a86e75b2fb97b34.png)

Photo by [John Schnobrich](https://unsplash.com/@johnschno?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 路线路径和参数

除了指定要映射到处理函数的 URL 之外，还可以指定路由路径。路由路径是可以包含命名参数的字符串，命名参数是将传递给处理函数的值的占位符。

例如，假设我们有一个博客，我们想创建一个查看单个帖子的路径。我们可以创建一条这样的路线:

```
app.get(‘/posts/:postID’, (req, res) => { // Get the post with the specified ID from the database // send it as the response})
```

在这个路由中，我们定义了一个名为 postID 的命名参数。当向该路由发出请求时，postID 的值将作为 req 对象的属性传递给处理函数。

例如，如果向`‘/posts/123’`发出请求，那么`req.params.postID`将等于`‘123’`。这使我们能够轻松地获得关于我们想要查看的帖子的信息。

您可以在路由路径中定义任意数量的命名参数，它们都将作为`req.params`对象的属性传递给处理函数。

## 路线处理程序

正如我们上面提到的，路由处理程序是在向映射到它们的 URL 发出请求时调用的函数。这些函数是回调函数，它们通常接受两个参数 req 和 res。有时，路由处理程序可能接受下一个参数，该参数用于绕过或委托给下一个路由处理程序。

req 对象表示向服务器发出的请求，并包含有关请求的信息，如 URL、标头和正文。res 对象表示将被发送回客户机的响应，并允许您设置响应的状态代码、标头和正文。

```
app.get(‘/’, (req, res) => { // Set the status code to 200 (OK) res.status(200) // Set the content type header to ‘text/plain’ res.set(‘Content-Type’, ‘text/plain’) // Send a string message as the response res.send(‘Hello, World!’)})
```

上面的代码定义了一个简单的路由处理程序，它在将消息作为响应体发送之前设置响应的状态代码和内容类型。

## 结论

路由处理函数非常有用，因为它们允许您为不同的 URL 路径定义应用程序的行为。现在，您已经了解了 Express 中路由的基本知识！我希望这篇文章能教会你一些东西。祝你的编码项目好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*