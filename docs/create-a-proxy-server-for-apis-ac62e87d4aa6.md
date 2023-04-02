# 为 API 创建代理服务器

> 原文：<https://javascript.plainenglish.io/create-a-proxy-server-for-apis-ac62e87d4aa6?source=collection_archive---------1----------------------->

![](img/ab34cf01f1234a0163a700e847806bbf.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 在 Typescript 中创建代理服务器

今天，我们将在 Nodejs Typescript 版本中创建一个代理服务器。我们将有一个端点，它将被重定向到某个外部路由，并从它们的端点返回一个响应

## 什么是代理？

你可能会问什么是代理。以及我们为什么需要它。所以基本上任何到你的 URL 的路径都会被其他代表你的 URL 所服务。例如，假设我们有一个名为`https://api.any-orm.com/lead/create`的路径，但是你不希望你的终端用户看到这个请求，相反，它应该从`POST https://your-url.com/orm/lead`开始导航，而不要让用户感觉离开网站。

这个例子是一个特定的路线，但你也可以代理任何路线，如`https://api.any-orm.com/lead/*`到你的后端`[https://your-backend.com/orm/lead/*](https://your-backend.com/orm/lead/*)`

## 开始

现在我们对什么是代理有了一个概念，所以我们可以开始在项目中实现它。在本教程的帮助下，我已经创建了快速 ts 入门应用程序，因此您也可以遵循它

[](https://blog.logrocket.com/how-to-set-up-node-typescript-express/) [## 如何用 Node.js 和 Express - LogRocket Blog 设置 TypeScript

### 当您构建用 JavaScript 编写的服务器并使用 Node.js 和 Express 时，开发的简易性是非常好的。但是…

blog.logrocket.com](https://blog.logrocket.com/how-to-set-up-node-typescript-express/) 

现在让我们把注意力集中在代理上。我们将代理 5 个方法，包括指向端点`/proxy`的`GET, POST, PUT, PATCH, DELETE`

每当有人访问网站`http://localhost:8000/api/proxy`时，所有的请求都会被重定向到`https://reqres.in/api`

## 第一步-创建路线

我们在指向我们的`proxyRequest`函数的* route 之后发出了所有请求，该函数将接收请求和响应。在文章中，我们有时会写`proxyRequest`的实现

```
import { Router } from "express";
import proxyRequest from "./request";
const router = Router();

router.get('/*', async (req, res) => await proxyRequest(req, res));
router.post('/*', async (req, res) => await proxyRequest(req, res));
router.put('/*', async (req, res) => await proxyRequest(req, res));
router.patch('/*', async (req, res) => await proxyRequest(req, res));
router.delete('/*', async (req, res) => await proxyRequest(req, res));

export default router
```

## 第二步—复制所需的标题

代理的一部分意味着网站的行为应该与实际的网站类似，这也意味着所有需要的头也应该只在那个时候被接受，并在我们有请求时被复制

```
import { IncomingHttpHeaders } from "http";
import { Request, Response } from "express";
import fetch, { Headers } from "node-fetch";

async function copyRequiredHeaders(incomingHeaders: IncomingHttpHeaders): Promise<Headers> {
  const localHeaders = new Headers();

  // Preserve the Accept header
  if (incomingHeaders["accept"]) {
    localHeaders.append("accept", incomingHeaders["accept"]);
  }

  // Preserve If-Match
  if (incomingHeaders["if-match"]) {
    localHeaders.append("if-match", incomingHeaders["if-match"]);
  }

  // Preserve Content-Type
  if (incomingHeaders["content-type"]) {
    localHeaders.append("content-type", incomingHeaders["content-type"]);
  }

  return localHeaders;
}
```

同样为了简单起见，我只处理了三个主标题`accpet, if-match, content-type`，但是如果需要的话，你也可以创建更多的部分

现在，头部被复制，我们可以创建一个请求并管理它的响应

## 第三步—创建请求并管理响应

首先，我们将通过用实际路径和域替换我们的路径来创建一个 URL，然后我们将从`req.headers`复制所需的头，然后如果您想要发送任何自定义数据或任何凭据，您可以发送它，否则我们将获取请求。

`node-fetch`相当于来自浏览器的`fetch` API，这意味着在响应的第二阶段，我们需要检测我们想要生成什么类型的响应。在我们的例子中，我们想要与用户想要的相同的响应，所以我们将使用`response.headers`来确定使用`buffer`方法的响应。稍后，如果您想再次向客户端发送更多的数据，那么您可以在响应中设置并返回值

```
export default async function proxyRequest(req: Request, res: Response): Promise<void> {
  const url = req.path.replace("/proxy", ``);
  const domain = 'https://reqres.in/api'
  const newUrl = `${domain}${url}`;
  const headers = await copyRequiredHeaders(req.headers);
  const authData = {
    token: 'attached custom token', // amy data you required
    date: new Date().toUTCString()
  }

  const response = await fetch(newUrl, {
    method: req.method,
    headers: {
      ...headers,
      Authorization: authData.token,
      "x-version": "2016-07-11",
      "x-date": authData.date,
    },
    body: req.method !== "GET" ? JSON.stringify(req.body) : undefined,
  });

  const responseType = response.headers.get("content-type") ?? "application/json";
  const bodyData = await response.buffer();
  res
    .status(response.status)
    .type(responseType)
    .set({
      "request-id": response.headers.get("request-id"),
      "client-request-id": response.headers.get("client-request-id"),
    })
    .send(bodyData);
}
```

## 让我们测试

为了在运行应用程序后测试这一点，我们可以转到`http://localhost:8000/proxy/users`，它将指向实际路线`https://reqres.in/api/users`，并将返回相应的数据

## 结论

这将是它，现在每个请求将从`reqres.in/api`服务，你也可以自定义它。

有一些重要的事情需要注意，您应该只为最终用户代理开放 API、路由或受保护的 REST APIs，以避免任何网关或 cors 错误。此外，您只能在一定程度上定制身份验证机制，例如，如果路由受到 oAuth 的保护，那么您将不得不在您的终端管理它的令牌，并为下一个请求处理它们，这可能会成为一个管理难题

我希望您今天学到了一些新的东西，并在将来的类似用例中使用它。可以在 [ts-proxy repo](https://github.com/Piyush-Use-Personal/ts-proxy) 和快乐编码中找到源代码！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****