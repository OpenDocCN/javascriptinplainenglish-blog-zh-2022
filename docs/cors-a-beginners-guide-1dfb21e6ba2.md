# CORS:初学者指南

> 原文：<https://javascript.plainenglish.io/cors-a-beginners-guide-1dfb21e6ba2?source=collection_archive---------3----------------------->

理解为什么您总是从这里得到这个 cors 错误:

![](img/71dfbf4c8c0f542181b92809b6d9e326.png)

[source](https://www.pexels.com/photo/1-1-3-text-on-black-chalkboard-374918/)

如果你是一名网络开发人员，你可能听说过 CORS，但你可能不完全理解它是什么或为什么它很重要。在这篇博客中，我们将进一步了解 CORS，以及它是如何影响你的 web 开发项目的。

## 什么是 CORS？

CORS 是一种机制，它允许 web 服务器向来自不同来源(即域)的网页提供资源，而不是网页所来自的来源。例如，如果一个网页位于 example.com，它向 api.example.com 发出 HTTP 请求，该请求将被视为“跨来源”请求。

## 为什么 CORS 很重要？

在过去，web 浏览器实施同源策略，这意味着网页只能访问该网页来自的同一域的资源。这样做是出于安全原因，以防止网页访问其他域的敏感信息。

然而，这种同源策略也产生了意想不到的后果，限制了 web 开发人员构建真正创新和交互式 web 应用程序的能力。有了 CORS，web 开发人员现在可以访问来自其他域的资源，只要托管这些资源的服务器允许。

## CORS 是如何工作的？

当一个网页发出跨源请求时，浏览器向服务器发送一个带有“源”头的 HTTP 请求。然后，服务器可以根据“Origin”头的值和服务器的 CORS 策略决定是否允许该请求。

如果服务器允许请求，它会发送一个带有“Access-Control-Allow-Origin”头的 HTTP 响应。该头的值指定了允许访问资源的来源。例如，如果“Access-Control-Allow-Origin”报头的值是“[https://example.com](https://example.com/)”，那么只有位于 example.com 的网页才被允许访问该资源。

## 我如何实现 CORS？

如果您是 web 开发人员，您可以通过在跨源请求的 HTTP 响应中设置“Access-Control-Allow-Origin”头，在 web 服务器中实现 CORS。该头的值可以设置为“*”，以允许来自任何域的请求，或者您可以指定允许访问资源的特定域或域列表。

例如，在 Node.js 服务器中，您可以使用“CORS”NPM 包轻松设置“Access-Control-Allow-Origin”头:

```
const cors = require('cors');

app.use(cors());
```

在其他 web 服务器中，您可能需要使用不同的方法来设置“Access-Control-Allow-Origin”头。有关更多信息，请参考您的 web 服务器的文档。

## 结论

CORS 是一种重要的机制，它允许 web 服务器为来自不同域的网页提供资源。它使 web 开发人员能够构建更具创新性和交互性的 web 应用程序，同时仍然保持对敏感信息的安全性和控制。通过在 web 服务器上实现 CORS，您可以释放 web 开发项目的全部潜力。

如果你想深入了解 [CSS flexbox](https://gumroad.com/a/381209427/GHwFS) ，看看这本[电子书](https://gumroad.com/a/381209427/GHwFS)

关注我这里:)[阿达什·古普塔](https://medium.com/u/4323d7b9f6b1?source=post_page-----1dfb21e6ba2--------------------------------)以及[推特](http://twitter.com/adarsh____gupta)。

如果你愿意，你可以给我买杯茶来支持我。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。***