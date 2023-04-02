# 如何修复 Node.js 中的“413 请求实体太大”错误

> 原文：<https://javascript.plainenglish.io/how-to-fix-413-request-entity-too-large-error-in-node-js-226c0070e4f4?source=collection_archive---------2----------------------->

## 解决 Express 中的 HTTP“413 有效负载过大”错误

![](img/a34676f8d35c20992047b84b9f38fa8e.png)

Photo by [Felix Mittermeier](https://unsplash.com/@felix_mittermeier?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我最近不得不处理“413 请求实体太大”的快递错误。经过一些研究，我发现这是一个相当常见的问题，可能有两个原因。在这两种情况下，当客户端发出被认为太大的请求时，服务器都会引发错误。

现在，让我们来学习关于“413 请求实体太大”错误的所有知识，并看看如何在 Express 中修复它。

# 什么是“413 请求实体太大”错误？

如 [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/413) 中所解释的，HTTP `413 Payload Too Large`响应状态码表示客户端执行的请求实体大于服务器定义的限制。因此，服务器可能会关闭连接或返回一个`[Retry-After](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After)`头字段。

HTTP `413 Payload Too Large`以前叫`[413 Request Entity Too Large](https://www.rfc-editor.org/rfc/rfc2616#section-10.4.14)`。请注意，大多数系统仍然这样称呼它。因此，如果您遇到“请求实体太大”的错误消息，您可以假设您正在处理一个 HTTP `413 Payload Too Large`错误。

# 为什么会出现 HTTP 错误 413？

如前所述，当客户端请求大于服务器愿意或能够处理的请求时，会出现 HTTP 错误 413。具体来说，这可能是因为两个原因。让我们深入研究一下。

## 1.Web 服务器配置不佳

由于客户端请求超出了 web 服务器配置中定义的大小限制，您会得到一个 HTTP 错误 413。例如，[缺省情况下，Nginx 强加的客户机请求大小限制被设置为 1 MB](http://nginx.org/en/docs/http/ngx_http_core_module.html#client_max_body_size) 。因此，如果您没有配置 Nginx 来显式地期望一个更大的值，那么对于任何大于 1MB 的请求，您都会得到一个 HTTP 错误 413。

## 2.配置不佳的应用服务器

您会得到一个 HTTP 错误 413，因为客户机请求超过了应用服务器配置中定义的大小限制。例如，Node.js 服务器上的 Express 应用程序默认将 JSON 请求体限制为 100Kb。因此，如果没有将 Express 配置为显式地期望一个更大的值，那么对于任何大于 100Kb 的 JSON 请求，都会得到 HTTP 错误 413。

在本文中，您将了解如何解决由第二个原因导致的 HTPP 413 错误，即糟糕的应用服务器配置。如果你想深入研究第二个原因，[看看这篇文章](https://betterprogramming.pub/how-to-fix-error-413-in-apps-behind-nginx-on-aws-elastic-beanstalk-c68a1ef2c331)。

[](https://betterprogramming.pub/how-to-fix-error-413-in-apps-behind-nginx-on-aws-elastic-beanstalk-c68a1ef2c331) [## 如何修复 AWS Elastic Beanstalk 上 Nginx 后面的应用程序中的错误 413

### 解决了使用 Nginx 作为反向代理时“413 请求实体太大”的错误

better 编程. pub](https://betterprogramming.pub/how-to-fix-error-413-in-apps-behind-nginx-on-aws-elastic-beanstalk-c68a1ef2c331) 

# 修复 Express 中的“413 请求实体太大”错误

要修复 Express 应用程序中的“413 请求实体太大”错误，只需更新服务器初始化文件。这通常称为`index.js`或`server.js`，是您初始化 Express 服务器的地方。确保该文件包含以下行:

最后两行代码将 JSON 有效负载和 URL 查询参数的大小扩展到 10MB。这应该足以避免您的 Express 应用程序中的大多数“413 请求实体太大”错误。根据您的需要配置这两个极限值，但不要不必要地加大它们的尺寸。

瞧啊！您刚刚学习了如何在 Node.js Express 应用程序上解决“413 请求实体太大”错误。

# 结论

在本文中，您了解了什么是 HTTP 错误 413，它为什么会出现，以及如何解决它。具体来说，您看到了如何在 Node.js Express 服务器上修复“413 请求实体太大”。当客户端请求比服务器预期的要大时，这是一个特别常见的问题。如图所示，只需要几行代码就可以解决这个问题。

感谢阅读！我希望这篇文章对你有所帮助。请随意留下任何问题、评论或建议。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***