# Node.js 开发人员的 3 个 YouTube 视频

> 原文：<https://javascript.plainenglish.io/3-youtube-videos-for-node-js-developers-7b4a98498ef7?source=collection_archive---------9----------------------->

## 我向每个 Node.js 开发者推荐的 YouTube 视频

今天，我想和你分享 YouTube 上的三个视频，我推荐给每一个想要了解更多关于 Node.js、JavaScript 和 TypeScript 的 Node.js 开发者。

![](img/3b84a74a6291b17e91ad439ca42411ec.png)

Photo by [Alexandru Acea](https://unsplash.com/@alexacea?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# Node.js 事件循环:不是单线程的

2017 年，[布赖恩·休斯](https://medium.com/u/3bbd87f7acb7?source=post_page-----7b4a98498ef7--------------------------------)做了一场关于 [Node.js](https://github.com/nodejs/node) 的精彩演讲，并宣布了一篇让 NodeJS 社区充满好奇的论文。他声称 Node.js 并不像我们想象的那样是单线程的。但是看了他的演讲后，你很可能会同意他的观点，因为他提到了事实。

用 C 编写的 Libuv 提供了 Node.js 的事件循环。一些异步任务(回调)将被外包给事件循环线程池，该线程池不是单线程的，因为 C 是一种多线程编程语言。

总之，是的，我们的 Node.js 根代码是单线程的，但是 Libuv 和我们的回调函数不是单线程的。很棒的谈话。我强烈推荐多看一遍他的视频。试试看。

最近，受来自[布赖恩·休斯](https://medium.com/u/3bbd87f7acb7?source=post_page-----7b4a98498ef7--------------------------------)的视频的启发，我写了一篇关于 Node.js 及其事件循环的文章。看看这个。

[](https://blog.bitsrc.io/node-js-event-loop-and-multi-threading-e42e5fd16a77) [## NodeJS &事件循环:不是单线程的

### Node.js、事件循环和多线程

blog.bitsrc.io](https://blog.bitsrc.io/node-js-event-loop-and-multi-threading-e42e5fd16a77) 

# 为什么我对打字稿的看法是错的

[TJ VanToll](https://medium.com/u/c944c796704?source=post_page-----7b4a98498ef7--------------------------------) 在 2019 年发表了一场激动人心的演讲，时不时的谈谈自己对 TypeScript 的看法。当他第一次听说 TypeScript 时，他并没有被迷住，因为 TypeScript 本身并没有完全说服他。

无论如何，TJ 万托尔当时有他合理的怀疑。他试图说服他的公司 [Native Script](https://github.com/NativeScript/NativeScript) 不要依赖 TypeScript，因为它并不流行。我不想太宠。自己带个表就行了。值了。对他来说，谈论这些年来他的观点的改变以及他现在对打字稿的看法是令人兴奋的。

非常棒的见解！

[](https://blog.bitsrc.io/solid-principles-in-typescript-153e6923ffdb) [## 带打字稿的固体原理(2022)

### TypeScript 对用 JavaScript 编写干净的代码产生了巨大的影响。但是总有办法…

blog.bitsrc.io](https://blog.bitsrc.io/solid-principles-in-typescript-153e6923ffdb) 

# 幕后的 NestJS

流行的 TypeScript web 框架 [NestJS](https://nestjs.com/) 的创造者和策划者 Kamil Mysliwiec 讲述了 NestJS 如何在幕后工作。这是每个 Node.js 后端开发人员的必看之作，因为 NestJS 是 Node.js 后端开发的必由之路。

## 什么是 NestJS？

您从未听说过 NestJS: NestJS 是一个用于构建高效、可伸缩的 Node.js web 应用程序的框架。它使用现代 JavaScript，是用 TypeScript 制作的。如果您开发一个用 TypeScript 构建的 API，那么 NestJS 是一个不错的选择！它深受春天和棱角的启发。

我从 2018 年开始与 NestJS 合作，我很喜欢它。我清楚地记得，在测试了一周左右后，我想知道为什么它在 Github 上只有 6k 或 7k 星，因为它过去是，现在仍然是 NodeJS 后端社区的绝对游戏规则改变者。

我强烈推荐这个视频，甚至推荐给可能坚持使用 Express 或其他 web 框架的开发人员。

想了解更多关于 NestJS 的信息？请阅读我关于如何在 NestJS 中构建简单 API 的文章。看一看。

[](https://blog.bitsrc.io/how-to-build-a-simple-api-in-typescript-with-nest-js-876386b29753) [## 用 NestJS (2022)在 TypeScript 中构建一个简单的 API

### 关于如何在 TypeScript 中构建 NestJS API 的简要指南

blog.bitsrc.io](https://blog.bitsrc.io/how-to-build-a-simple-api-in-typescript-with-nest-js-876386b29753) 

感谢您阅读我关于 YouTube 视频的文章。我向每个 Node.js 开发者推荐它们。我希望你和我一样喜欢这些视频。

干杯！

我希望你喜欢读这篇文章。如果你愿意支持我这个作家，可以考虑让[成为一名灵媒](https://medium.com/@hellokevinvogel/membership)。每月只要 5 美元，你就可以无限制地使用 Medium。

想支持我？请帮我买一杯[咖啡](https://www.buymeacoffee.com/hellokevinvogel)。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*