# 用 Fetch API 发出 AJAX 请求

> 原文：<https://javascript.plainenglish.io/make-ajax-requests-with-the-fetch-api-9c8add20ba64?source=collection_archive---------7----------------------->

大多数 web 应用程序、应用程序和网站都是基于一些协会提供的 API 和服务，或者是为特定目的而开发的。这些服务非常有用，如果没有它们，大多数资源都不会存在。

因此，在本文中，我们将探索如何通过 Fetch API 调用所有 API，这样您就可以检索您需要放在网站上的所有信息。

![](img/09db9552347bec887b341fff4c2d7dda.png)

# 介绍

首先你要知道用 Fetch 做调用和通过`jQuery.ajax()`做调用是不一样的，即使结果是一样的。

不同之处在于:

*   使用 Fetch API，返回的承诺不会被拒绝，即使有类似 404 的响应代码。它的工作方式是一样的，在状态中添加 OK 或 false。
*   如果没有明确请求，Fetch 不会发送跨来源 cookies。

对于它如何工作的一般概述，我们可以说 Fetch 使用 HTTP 协议，因此它处理请求和响应。如果您需要更多关于 HTTP 的信息，请阅读这篇文章:

[](/http-protocol-everything-you-need-to-know-d313b5544c93) [## HTTP 协议:您需要知道的一切

### 如果你曾经在浏览器上搜索过网页，你肯定至少曾经使用过这种特殊的协议…

javascript.plainenglish.io](/http-protocol-everything-you-need-to-know-d313b5544c93) 

了解协议的所有细节并不是强制性的，但这很有用。尤其是涉及到状态码的时候。

Fetch 是一个异步函数，它返回一个承诺，该承诺被解析为对您之前设置的请求的响应。

# 接口

此 API 有一些接口，如下所示:

```
fetch()
Headers
Request
Response
```

Fetch 是用来获取资源的方法，我们将在后面看到。在 HTTP 协议中，头是响应/请求的头。请求包含请求信息和响应信息。

# 和睦相处

Fetch API 与几乎所有现代浏览器都兼容。只有 IE 浏览器不能正常处理这个 API，但是现在 IE 几乎已经消失了。

所以，如果你需要调用一个 API，这是最好的选择，也是根据可用的设备和浏览器。

# 如何发出 GET 请求

现在，我们可以深入了解如何使用 fetch API 从互联网和全球各地的服务中检索信息。HTTP 的第一个方法将是最著名和最常用的:GET 方法。

根据动态数据库的发展，当有人想要接收数据以显示在 UI 中时，就使用 GET。

在 Fetch API 中，GET 是默认方法，因此这是最简单的操作。您只需要指定到 API 端点的链接。

这里有一个代码示例，用于执行对随机 API URL 的调用，您可以根据自己的脚本进行调整:

```
fetch('http://www.apiwebsiterandom/getinformations')
    .then(response => response.json())
    .then(data => console.log(data)
```

在这个例子中，它调用一个随机的 API(这是假的)到一个给定的路由。它创建一个异步工作的承诺，并在解析后返回一个字符串。

此时，您创建了一个新的承诺，它将字符串异步转换为 JSON。JSON 是获取 API 使用的基本格式，但是它是可以改变的。

然后，结果是您可以使用对象作为响应来动态生成您的数据。

# 如何提出发布请求

第二个最重要的方法是 POST，它允许用户将信息放入 API，最终放入数据库。

这是一个特殊的方法，因为你可以添加一个主体来放置几乎对所有人都隐藏的所有信息。

这不是 API 的默认方法，所以我们必须在函数体中指定它。

我们可以在这个函数中设置很多值，稍后我们会看到。现在，我们将只看到方法和主体。它们允许我们设置使用什么 HTTP 方法，以及主体的内容。

以下是 POST 请求的语法:

```
fetch('http://www.apiwebsiterandom/postnews', { method: 'POST', headers: { 'Accept': 'application/json', 'Content-Type': 'application/json' }, body: JSON.stringify({          username: username, password: password})})
    .then(response => response.json())
    .then(data => console.log(data)
```

此外，还使用了 heather 方法，它表示 JSON 是默认的响应格式。

作为一种方法，我们使用 POST，但是你可以使用所有大写的 HTTP 方法。在正文中，您需要放入一个字符串化的 JSON，其中包含您想要发送的最终数据。

# 发出普遍呼吁

也许你想对 API 进行一般性调用。这里有一个方案，几乎所有的东西，你可以修改和个性化，并附有简要说明。

有了这个方案，您将能够以最好的方式管理对 API 的所有调用。

```
fetch(url, {
    method: 'POST', // GET, POST, PUT, DELETE, HEADER .....
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload,... for cached information on the call
    credentials: 'same-origin', // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json' // type of content 
    },
    redirect: 'follow', // manual, *follow, error... if you need a redirection 
    referrerPolicy: 'no-referrer', // no-referrer, *no-referrer-when-downgrade, origin... reffers to the policy 
    body: JSON.stringify(data) // same type of headers one
})
    .then(response => response.json())
    .then(data => console.log(data)
```

您只需要定制这些信息，就可以调用每一个可能的 API 并检索您正在搜索的有用数据。

# 结论和正式文件

通过这篇文章，您已经掌握了关于 Fetch API 的所有最重要的信息。您的站点或应用程序现在可以拥有它需要的动态数据。

如果您需要更深入的文档，请查看以下链接中的文档:

[](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) [## 使用获取 API-Web API | MDN

### Fetch API 提供了一个 JavaScript 接口，用于访问和操作 HTTP 管道的各个部分，例如…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*