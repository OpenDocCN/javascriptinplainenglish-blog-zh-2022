# 网络安全:什么是 CORS？

> 原文：<https://javascript.plainenglish.io/web-security-what-is-cors-4f38aefdb454?source=collection_archive---------9----------------------->

![](img/d0e5d1eea3b31dfaff4afe1e6bae0c68.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你从事 web 开发已经有一段时间了，你可能听说过“CORS”这个术语但是到底是什么呢？你为什么需要知道它？在这篇博文中，我们将讨论什么是 CORS，以及它如何帮助提高网站的安全性。

## 定义 CORS

CORS，缩写为“跨源资源共享”，是一种允许不同域之间共享资源的机制。CORS 指示哪些域可以从浏览器向服务器发出某些请求。例如，如果域 A 上的网站想要向域 B 发出请求，则必须配置 CORS，以便浏览器允许该请求。

## 什么是 CORS 政策？

CORS 策略是一组指示允许来自哪些域的哪些请求的指令。当浏览器向服务器发出请求时，服务器将检查 CORS 策略，以确定是否允许该请求。如果请求被允许，服务器将处理请求并返回适当的响应。如果请求不被允许，浏览器将收到一条错误消息。

CORS 政策可以非常简单，也可以非常复杂，这取决于你的网站的需求。例如，一个简单的 CORS 策略可能允许来自任何域的所有请求。更复杂的策略可能只允许来自特定域的某些类型的请求。

![](img/85f9dd945cbcbca0bbd6c6c8ea7919df.png)

Photo by [Aleksander Vlad](https://unsplash.com/@aleksowlade?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## CORS 是如何工作的？

为了确保要发送的数据是安全的，在发送实际请求之前，会向服务器发出预检请求。该请求中将包含源标头。然后，服务器将评估该请求，以确定它是否安全。服务器将发回一个包含 Access-Control-Allow-Origin 报头的响应。

如果 Origin 头的值与 Access-Control-Allow-Origin 头的值匹配，浏览器将继续处理请求。否则，浏览器将阻止该请求，用户将收到一条错误消息。

## 为什么 CORS 很重要？

CORS 是一个强大的工具，可以帮助提高您的网站的安全性。通过仔细配置您的 CORS 策略，您可以控制允许哪些域向您的网站发出请求。这有助于防止恶意域发出未经授权的请求，这些请求可能会危及您网站的安全。

如果客户在检查您的 CORS 政策后未被批准，该客户将无法访问您网站的数据和资源。因此，CORS 有助于降低网站安全漏洞的几率。

## 结论

在这篇文章中，我们简要介绍了 CORS。我们已经定义了什么是 CORS 政策，它是如何运作的，以及它为什么重要。我希望这篇文章能教会你一些东西。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***