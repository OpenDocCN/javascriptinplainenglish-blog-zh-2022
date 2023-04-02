# 用于服务间通信的 NATS 流 Node.js 示例

> 原文：<https://javascript.plainenglish.io/nats-streaming-for-inter-services-communication-nodejs-example-17a40ea4e45d?source=collection_archive---------6----------------------->

## 微服务范例中服务之间的内部通信。

![](img/d883ae6c39624e913722b5c1cb83f464.png)

Photo by [Chris Ried](https://unsplash.com/@cdr6934?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

微服务设计使您能够构建独立的服务，每个服务负责其数据库、错误处理、部署等。这些组件作为一个系统协同工作。

尽管本文主要关注的是微服务范例中服务之间的内部通信，但是稍微了解一下微服务最常见的架构模式也很重要。

# **微服务的模式**

*   同步:等待，直到响应可用
*   异步:不需要等待响应

由于我的首选模式是异步模式，因此本文将主要关注通过使用消息总线管理服务间通信而编排的异步事件。

# 什么是事件总线？

允许不同系统基于特定规则和公共数据模型进行通信的消息传递基础设施。

# 什么是 NATS 河？

NATS 是一个数据流系统，用于跨云供应商、内部、web 和移动以及设备的任意组合进行安全通信。

在本文中，我们将讨论 NATS 在同一网络(K8s 集群)下基于 Docker 的容器化服务之间的内部通信中的使用。

为了便于理解，必须确保我们可以在本地开发和测试数据流，为此，我们已经准备了关于如何准备 NATS 流及其不同部分的完整文档。

请注意，我们的示例应用程序将使用 Nodejs 和 Typescript 编写。

# 我们走吧

让我们从 NATS 的本地部署 YAML 文件开始:

现在，准备好 NATS 流基础设施后，我们需要创建以下主要部分:

*   连接:连接到 NATS 客户端
*   发布者:能够在 NATS 流上发布事件
*   侦听器:能够侦听 NATS 流上的事件

# 创建 NATS 连接

在连接到 NATS 之前，我们需要创建包装器，以确保我们每次都使用同一个客户端。

下面是 NATS 包装器的单例实现的示例:

现在，是时候从你的入口连接到 NATS 了。

连接到 NATS 后，我们可以根据需要使用我们的发布者和侦听器，这需要发布者和侦听器使用相同的主题，以便向相关的发送者和接收者发送事件。

在使用任何数据流基础架构时，注意两点非常重要:

*   OCC(乐观并发控制):用异步事件处理并发
*   队列组([此处阅读](https://docs.nats.io/nats-concepts/queue))

这篇文章的灵感来自斯蒂芬·格里德关于 NATS 流媒体的精彩演讲。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**