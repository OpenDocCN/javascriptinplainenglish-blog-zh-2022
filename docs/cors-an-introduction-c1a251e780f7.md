# CORS:简介

> 原文：<https://javascript.plainenglish.io/cors-an-introduction-c1a251e780f7?source=collection_archive---------11----------------------->

## 什么是**跨源资源共享** ( **CORS** )，它是如何工作的，如何利用全栈开发中最大的误差源

![](img/751ec4bfa11955f61959dbccc3ec1c46.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske) on [Unsplash](https://unsplash.com/s/photos/bugs-in-programming)

如果你曾经有过开发全栈网站的经验，你可能会接触到跨源资源共享(CORS)。

当您在机器上开发并测试后端如何响应前端(反之亦然)时，会发生很多次 CORS 错误，从而阻止整个代码运行。

许多开发人员在没有真正了解他们正在处理什么以及应该如何管理它的情况下处理它。理解 CORS 也很重要，因为现在它已经在大多数浏览器中实现了。

所以，让我们来发现它是什么。

## 什么是 CORS？

CORS 是一个首字母缩写词，意思是跨原产地资源共享。

这意味着每次你试图在你的网站上，用一个 X 网址，从一个 Y 网址请求各种资源。一个典型的例子是 foo.com 的*网站*向 bar.com 的*网站*请求想要的图片。

它基于 HTTP 协议，其机制基于协议提供的报头。它检查请求实体是否有权获得所请求的资源。

每次在 Javascript 中执行 *fetch()* 或 *XMLHTTPRequest* 时，你都在使用 CORS。

## 它是如何工作的？

CORS 机制，根据主要的和编程的规则，如果调用实体可以检索它想要的图像，到它需要的数据集。

这可以通过操纵源(域、端口、方案)或一些其他设置来完成，包括所需数据的类型或请求的类型。

因此，您可以将它视为一个过滤器，根据您的需要只接受某些类型的请求。

要完全理解这种机制，您需要知道一些要点。它们是:

**同源政策**

几乎每个浏览器都采用了 CORS 带来的隐私政策。该特定政策的要点是同源政策。

这意味着 CORS 允许来自相同来源的请求，并与它们自由共享资源。它还会阻止来自外部 URL 的任何内容，除非符合某些要求。

**预检**

这是一个简单的概念。这意味着某些类型的信息是完全不允许的，因此根本无法生成响应。

通常，一些像 PUT 或 PATCH 这样的方法是从服务器上预加载的，所以没有人能接触到这些内容。这只能从服务器本身进行更改，或者在可能的情况下通过更改请求进行更改。

**访问控制允许来源**

服务器使用这个特定术语来检查传入的请求是否来自有权检索资源的客户端。

它通常是一个 URL 列表或一个通配符。

当服务器收到请求时，它会生成响应，并动态设置这个特定的属性。此时，服务器需要检查请求的来源是否与响应相同。

如果是，则没有问题，并且发送响应。否则，浏览器中会出现一个控制台错误，但只有一些安全问题的详细信息。所以，如果你不了解 CORS，这很难调试。

如果参数是通配符，则接受每个原点，但在其他音高中有一些限制。

这是一个接受请求的例子，因为源是允许的。

请求:

```
POST /doc HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0)
Accept-Language: en-us,en;q=0.5
Content-Length: 55
**Origin: https://foo.example**

--- DATA STREAM ---
```

回应:

```
HTTP/1.1 **200** OK
Date: Mon, 01 Dec 2008 01:15:40 GMT
**Access-Control-Allow-Origin: https://foo.example**

--- DATA STREAM ---
```

否则，将会显示 404 错误，并且没有与客户端共享的数据。

**访问控制允许方法**

它与我们讨论的最后一个 pitch 相同，但它指的是 HTTP 方法。它完全按照前面讨论的音高工作。

这是一个可能的不同方法的列表。这可能是我们正在讨论的响应行的一个示例:

```
**Access-Control-Allowed-Methods: GET, POST, HEADER, PUT, PATCH**
```

在这种情况下，如果我发出一个删除请求，它会被系统预先触发并产生一个错误。否则，它将传递此控制并继续创建响应。

**其他可能的 CORS“过滤器”**

您可以设置许多其他 CORS 音高，以避免收到服务器可以手动解决的不相关请求。以下是最著名的几个:

*   `Access-Control-Allowed-Headers`
*   `[Acc](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language)ess-Control-Max-Age`
*   `Accept-Language`
*   `Content-Language`
*   `Content-Type`
*   `Range`

## 为什么 CORS 会产生这么多错误？

正如我们前面说过的，当请求中应该包含的内容与请求中写入的内容不匹配时，就会产生 CORS 错误。

很多时候，开发人员倾向于忘记 CORS，因为它看起来很容易，而且在通过 HTTP 对服务器或 API 请求进行编程时，没有人关心它。

例如，如果你在 Node 中编程，要把 CORS 添加到你的网站中，你只需要两行代码就足够了，以后你可以完全忘记它。

```
const express = require('express');
const cors = require('cors');app = express();
app.use(cors());
```

为了管理这些错误，存在许多与 CORS 相关的问题的 StackOverflow 答案。大多数时候，他们依赖于降低规则的限制性，从而降低网站的安全性。

所以，如果你需要解决一个 CORS 错误，也要注意安全部分。

## 资源

*   [CORS 官方文件](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
*   [100 秒内 CORS](https://www.youtube.com/watch?v=4KHiSt0oLJ0)

## 想要连接吗？

```
Twitter: [https://twitter.com/MatteoPossamai_](https://twitter.com/MatteoPossamai_)
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*