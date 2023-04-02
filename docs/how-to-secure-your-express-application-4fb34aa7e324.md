# 如何保护您的快速申请

> 原文：<https://javascript.plainenglish.io/how-to-secure-your-express-application-4fb34aa7e324?source=collection_archive---------6----------------------->

## 后端开发人员的安全提示:保护 Express 应用程序的指南。

![](img/26cd5aea00c97983b52a501ee807bcdd.png)

source: unsplash

作为后端开发人员，确保后端应用程序的安全性是我们的职责。今天，我将向您展示一些如何保护我们的 Express 应用程序的技巧。那我们开始吧。

## 1.使用头盔

![](img/cd6f0fb664d58fb98e8e7564a8578ec0.png)

source: unsplash

头盔不是银弹，但它可以帮助保护 express 应用程序。这基本上是一个包，它是 14 个更小的中间件功能的集合，这些功能基本上设置了一个安全头，以防止攻击者的常见攻击，如**点击劫持**、**跨站脚本(XSS)、**和其他恶意攻击。所以我们可以使用头盔包来保护我们的 express 应用程序。

## **2。限制并发请求**

众所周知，dos 攻击现在非常流行，而且相对容易，但我们可以通过使用负载平衡器、Nginx 等外部服务，甚至 express-rate-limit 等软件包来实现速率限制，从而防止这种类型的攻击。

如果我们不能适当地处理有限的并发请求，那么我们的系统将由于 Dos 攻击而对真实用户不可用。

## 3.保护您的 express 依赖关系。

npm 确实是一个强大的 web 开发工具。我们在项目中使用了很多 npm 包。但有时这些 npm 包可能包含严重的安全漏洞，这可能是我们应用程序的一个线程。所以我们必须使用更新的软件包。我们可以检查 npm 审计来修复它们。

## 4.阻止跨站点请求伪造

![](img/d0ece89a794b5bfb1fe2991d49fceae5.png)

source: [https://www.asharpeye.com/](https://www.asharpeye.com/)

攻击者可以通过他们自己的站点将数据放入您的应用程序，方法是使用常见的网络钓鱼技术，这种技术基本上使用跨站点请求伪造。例如，攻击者在他们的站点上制作一个相似类型的网络钓鱼表单，它接受相似类型的输入并在您的应用程序中发出请求。

我们可以通过实现 CSRF 令牌来防止这种类型的伪造。当用户发出请求时，会生成一个新的 CSRF 令牌并将其添加到用户的 cookie 中。应将此令牌添加到输入值中，然后根据 CSRF 库对其进行检查。

## 5.防止暴力攻击。

![](img/0ab87d62e7fb66c1ab8360da7c9c9b25.png)

source: unsplash

有时，攻击者可能试图使用错误的凭据多次登录您的应用程序。基本上，他在尝试蛮力技巧。但是我们也可以通过实现一些基本步骤来防止攻击者的这种技术。例如，如果一个 IP 使用错误的凭据尝试了 10 次或 20 次，我们可以阻止它。有一种叫做[限速器-灵活](https://github.com/animir/node-rate-limiter-flexible)的打包机，你也可以试试。

感谢您的时间和阅读我的文章。如果你认为这是信息学，那么请鼓掌，并在评论中告诉我你的建议或提示。

跟我来 [**Fiverr**](https://www.fiverr.com/ruhul_1995/do-your-javascript-react-nodejs-api-mongodb-mern-stack) ，[**Linkedln**](https://www.linkedin.com/in/ruhulcse/) ， [**Twitter**](https://twitter.com/AvangerRuhul)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*