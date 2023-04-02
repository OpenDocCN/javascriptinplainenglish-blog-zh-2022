# v17.5 节点中的 fetch()—回顾

> 原文：<https://javascript.plainenglish.io/fetch-in-node-v17-5-a-review-a435346178af?source=collection_archive---------7----------------------->

![](img/60020e23f33ccc2becc91e08ca231e52.png)

Image from unspalsh

Node.js 已经[宣布](https://github.com/nodejs/node/pull/41749)他们正在引入对 fetch()的支持，作为 v17.5 的一个实验模块，它将广泛用于 v18 版本。

## fetch()是什么？

fetch() API 为获取资源提供了一个标准化的接口，通常是通过 HTTP。这是一个基于 promise 的客户端，支持许多高级 HTTP 特性，同时也关注最常见的场景:发送简单的 HTTP 请求。

在其核心，API 包括四个接口

*   [fetch()](https://developer.mozilla.org/en-US/docs/Web/API/fetch) —用于发起请求的入口点
*   [Headers 类](https://developer.mozilla.org/en-US/docs/Web/API/Headers) —处理 HTTP 请求/响应头实例
*   [请求类](https://developer.mozilla.org/en-US/docs/Web/API/Request) —表示出站请求实例
*   [响应类](https://developer.mozilla.org/en-US/docs/Web/API/Response) —表示传入的响应实例

## 为什么每个人都这么兴奋？

嗯，这意味着今后不再需要额外的模块，因为 Node.js 核心现在将支持 API。这消除了添加第三方库的巨大开销(例如..、 [Axios](https://www.npmjs.com/package/axios) 、 [node-fetch](https://www.npmjs.com/package/node-fetch) 等)，同时也信任他们在我们进行过程中应用任何类型的支持&漏洞补丁。

我设法测试了这个实验特性，这里有一些例子

首先，我的机器上需要 node v17.5。为此，我使用了 nvm(节点版本管理器)

注意，实验旗。它仍在开发中，将在 18 版中全面使用。

我执行了三个测试(GET、POST 和 DELETE)

## 得到

## 邮政

## 删除

他们都按照预期工作🎉请注意，我也不需要导入任何模块。这是因为 fetch 被添加为全局-[https://github.com/nodejs/node/pull/41749](https://github.com/nodejs/node/pull/41749)

这是更大计划中的一个小变化，但对于使用 Node.js 作为开发环境的每个人来说，它都有着巨大的意义。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*