# 如何成为完整的前端开发人员

> 原文：<https://javascript.plainenglish.io/how-to-become-the-complete-front-end-developer-7a9e3395ae8b?source=collection_archive---------11----------------------->

## 了解 HTML/CSS/JavaScript 有助于你开始前端开发。还有一些其他的因素可以帮助你坚持下去。

![](img/9ff4c65e5fbd0af7e780a746a8260588.png)

Photo by [Farzad Nazifi](https://unsplash.com/@euwars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

前端开发。投身于前端开发就像在海滩上看日落一样。你越想靠近它，它就越远。有很多框架、库和其他工具可以帮助前端开发。是的，HTML/CSS & JavaScript 方面的专业知识给了你优势，但是这里还有其他工具在发挥作用，这是我们在旅途中经常忽略/不太注意的。如果你是一名前端开发人员，下面的列表会对你有所帮助。

## **框架/库**

这一步实际上是在学习了 HTML/CSS & JavaScript 之后。你可以选择 Angular/React 这样的趋势框架，也可以选择为你的工作场所设计的框架。通常这些框架/库都带有模板代码。在编写 UI 组件之前，理解这些模板代码是如何工作的是必要的。

## **从服务器获取数据(API )**

所以。我们使用框架/库构建了屏幕。编写后端的人给了你一堆带有示例请求的 URLs 一些需要记住的事情。

*内容类型*

使用 API，您可以从服务器请求和接收特定的数据类型。大多数情况下，这默认为 *application/json* ( API 响应是一个 json 对象)。可能存在响应可能是 blob 对象或文本的情况。我们需要正确设置该属性，以避免内容类型错误。

*跨产地资源共享(CORS)*

我们需要理解服务器的 CORS 设置，其中前端和后端服务有效地在浏览器和服务器之间共享信息。用一两句话来解释 CORS 从来都不容易。在 [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) 网站上给出了一个简单而有力的解释。

*HTTP 响应状态码*

JavaScript 承诺的美妙之处在于——不管是好是坏，您总能得到回应。开始时，最好记住一般的 HTTP 代码，以便在每次遇到 API 错误时节省几分钟时间。

我经常遇到的一些标准 HTTP 状态码。

```
200 - OK // Everything went well
404 - Resource Not Found // Mostly, Wrong/Missing API endpoint
400 - Bad Request // Request Body is not correct
403 - Forbidden // Unauthorized to hit the API
415 - Unsupported Media Type // Check Content-Type in Header
500 - Internal Server Error // API error
503 - Service Unavailable // The API server is not available
```

## **安全**

我们到底在做什么？为网络构建产品和服务。是的。你的前端总是有被攻击的可能。了解常见的攻击(如 XSS、CSRF)和防范技术可以在您构建新站点/恢复旧站点时节省一些时间。在大多数情况下，我们使用的框架/库有助于缓解这种情况，但是开发人员需要决定是否使用任何易受攻击/不推荐使用的类，并在编码时遵循安全指南。

## **Node.js**

我们都知道 Node.js 是做什么的。我喜欢它在命令提示符下执行代码的能力。我们可以将复杂的逻辑放在一个 js 文件中，并在终端中验证它。有些 Node.js APIs，比如文件读/写，有时可能会派上用场。

```
node sample.js
```

Node.js 可以帮助您独立地编写方法——不需要 UI 来测试您的逻辑。

## **版本控制**

如今一切都围绕着 Git。了解 Git 如何操作将每天节省几分钟，主要是在与团队合作时。下面是一些需要知道的事情。

1.  列出所有最近的提交。
2.  藏起你的零钱。
3.  理解冲突
4.  重新确定提交的基础
5.  分支和合并
6.  检验

## **饼干**

最后但同样重要的是，饼干。大多数情况下，我们使用 cookies 进行会话管理/个性化。管理 cookies 有内部和外部的规则。所以，我们必须了解 cookies 在我们网站上的使用和实现。

## **结论**

上述列表可能并不详尽。其他东西，如托管基础设施及其配置和可用的第三方库，主要取决于您正在构建的产品/服务的性质。这些知识也会有所帮助。但是，对上面列表的基本理解应该有助于您在成为一名完整的前端开发人员的旅程中站稳脚跟。

编码快乐！

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*