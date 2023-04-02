# 如何创建 API 映射扩展

> 原文：<https://javascript.plainenglish.io/how-to-create-an-api-mapping-extension-65530cb98efa?source=collection_archive---------26----------------------->

![](img/d656326a05f141fd76f46db621fb2f5d.png)

Photo by [Jefferson Santos](https://unsplash.com/@jefflssantos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

所以问题来了。我们都喜欢制作粗糙的网页抓取器、网页扩展和其他很酷的东西。公平地说，这并不总是最容易做到的事情。不是所有的网站都有定义良好的 API 和文档，当你遇到困难时可以参考。

这是我想要解决的问题，所以在这个 devlog 系列中，我将通过在你使用网站时记录一个 API 来构建一个 web 扩展，让这个问题变得简单一些。我不知道这会有多难，我会尝试各种各样的新事物。在 devlog 0 中，我将为这个扩展定义计划，并选择我们的技术栈。

# **计划**

我想创建一个 web 扩展来捕获任何 web 请求(无论是 HTTP、web sockets 还是 WebRTC ),并创建一个 API 的粗略类型定义。此外，我希望能够导出这些“模式”并下载它们供以后使用。我想要一个很好的 devtools 界面来实时查看数据。

所以让我们稍微缩小一下，定义一个 MVP(最小可行产品)。我想去掉尽可能多的“额外特性”，所以我们只剩下组成扩展的最小特性集。首先，我们可以关注 HTTP 请求，因为它们是最常见的请求类型。我稍后会添加对其他人的支持，但这是为了尽快完成一个应用程序。虽然我也可以去掉 devtools 接口，只提供一个下载按钮，但我更可能使用 UI，而不是下载一个大的模式文件。

## **界面**

UI 将看起来类似于 network devtools 选项卡，因为您将看到一个请求表，但是我将只为每个端点呈现一个请求表，并且它们将根据发送它们的域划分为下拉列表。

此外，单击一个请求将显示关于端点的信息，并提供类型和一个“示例”，这实际上是发送到该端点的第一个/最后一个请求。

在[最近的一篇文章](/technologies-i-plan-to-learn-in-2022-a9f44e9c3162?source=user_profile---------0-------------------------------)中，我提到我想学习苗条身材，我认为这是一个尝试的好机会。

[](/technologies-i-plan-to-learn-in-2022-a9f44e9c3162) [## 我计划在 2022 年学习的技术

### 我 2022 年的学习目标。

javascript.plainenglish.io](/technologies-i-plan-to-learn-in-2022-a9f44e9c3162) 

**捕获 Web 请求**

将使用内容脚本捕获 Web 请求，并将其转发到后台脚本。然后，后台脚本将处理这些数据，并使用选项卡 id 存储这些数据。然后，devtools 脚本可以从后台脚本请求这些数据。

虽然我还没有添加对 web socket/RTC 请求的支持，但我想为了做到这一点，我会使用原型污染或者完全重新定义对象。尽管我需要注入一个脚本，这个脚本可能无法在有内容安全策略的网站上运行。

# **倒影**

我有一个清晰的计划，我将如何创造这一点，现在我只需要开始原型制作。下一次，我将构建消息传递接口和存储，并制作一个概念验证请求处理程序。我还将为 devtools 选项卡设置 Svelte 项目，并使用某种脚本将它与我的内容和背景脚本捆绑在一起。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。***