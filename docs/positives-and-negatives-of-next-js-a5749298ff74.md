# Next.js 的优缺点

> 原文：<https://javascript.plainenglish.io/positives-and-negatives-of-next-js-a5749298ff74?source=collection_archive---------2----------------------->

![](img/cc67bbad2252e83c0b04e80c8285a4d4.png)

开发网站应该是一种自由的体验。

如果你使用 high-code，可以自由选择你想使用的框架。

在 [Fathym 的可组合前端架构中，](https://www.fathym.com/blog/articles/2022/september/2022-09-01-explaining-composable-frontend-architecture-as-simply-as-possible)你可以使用任何 JavaScript 框架(甚至一些其他框架)来构建你的网站的一个方面。然后，如果你愿意，使用不同的框架，或者高代码、低代码和无代码构建器的组合。

太棒了，对吧？没错。

因此，本着传播可组合前端的精神——你可以与 [Fathym 的新 UI](https://www.fathym.com/blog/articles/2022/august/2022-08-08-introducing-fathyms-revamped-ui) 一起使用——我们来看看 Next.js 中的一个新框架

# Next.js 人气

我们深入研究了 StackOverflow 的 2022 年开发者调查，其中他们列出了最受欢迎的[框架。](https://www.fathym.com/blog/articles/2022/july/2022-07-13-ranking-javascript-frameworks-by-popularity-2022)

虽然 Svelte 在 2021 年排名第一，但它被 Phoenix Framework 超越，我们看到了许多其他新人，包括 Next.js。

令人惊讶的是，Next.js 是 2022 年用于前端开发的第五大流行框架，甚至比 React 排名第六。所以，很明显人们喜欢 Next 提供的东西。

![](img/6e48a31873238f17c5b5d275c87b5a9b.png)

框架的普及性很重要，原因有很多。

首先，如果你和你的团队正在进行一个长期的大项目，你需要确保你所使用的框架将贯穿整个过程。想象一下，开始一个重要的网站建设，而框架突然从地球上消失，那将是一场噩梦。

其次，这种受欢迎程度保证了更多的开发人员知道如何使用这个特定的框架。如果你的第一个开发人员离开了，你应该可以用另一个团队成员来填补他们的位置。或者，在我们的模块化前端的情况下，您可能希望同一个团队中的多个成员了解同一个框架。他们可以合作，互相帮助，创造一些特别的东西。

如果你的公司扩张，你将能够找到使用流行框架的新开发人员。

让我们来看看它是什么，它做什么以及 Next.js 的优点/缺点。

# Next.js 是什么？

Next.js 由 Vercel 的首席执行官 Guillermo Rauch 在 2016 年开发，目前版本为 12.2，将于 2022 年 6 月下旬发布。而 Next.js 实际上是在 Node.js 之上编写的，所以它要求你有 Node.js 才能和 Node Package Manager (npm)一起使用。

Next.js 的一个特性是它在服务器端和客户端的呈现方式，也称为“通用应用程序”这对它构建的单页面应用程序(SPAs)至关重要，它如何帮助这些 SPAs 在 SEO(搜索引擎优化)方面取得更大的成功。

正如搜索引擎优化专家巴瑞·亚当斯解释的那样:

“当您使用 React 而不使用服务器端呈现时，会发生的情况是，crawler 在第一页就停止了，因为它看不到任何要跟随的超链接。它将页面发送到索引器，索引器随后必须呈现页面并提取超链接，这些超链接随后将被添加到爬虫的队列中。然后，爬行器将最终爬行下一组页面，并再次在那里停止，因为所有链接都是不可见的，直到 JavaScript 被呈现。所以它必须等待索引器返回一组新的要抓取的 URL，”亚当斯在一篇媒体文章中解释道。

用最简单的话来说:SEO 对于任何一个想通过谷歌搜索发现自己网站的人来说都是至关重要的，Next.js 在这方面提供了巨大的帮助。水疗很棒，因为它们快速、灵活、适应性强。但是 SPA 的一个主要缺点是，因为它们大部分是在客户端呈现的，所以当 Google 的爬虫寻找数据时，它们找不到任何数据，直到它们也被呈现在服务器端。

Next.js 在客户端和服务器端都呈现:网站的部分或全部呈现在服务器端，因此 Google 的爬虫可以找到信息(URL、元标签和内容等)。)并因此将其放入搜索结果中。

“服务器端渲染(SSR)是一种流行的技术，用于在服务器上渲染通常只有客户端的单页应用程序(SPA)，然后将完整渲染的页面发送给客户端，”geeksforgeeks.org[解释道。](https://www.geeksforgeeks.org/node-js-server-side-rendering-ssr-using-ejs/#:~:text=js%20Server%20Side%20Rendering%20(SSR)%20using%20EJS,-View%20Discussion&text=Server%2Dside%20rendering%20(SSR),SPA%20can%20operate%20as%20normal.)。

为了帮助缩短加载时间并将代码分解成更小的块，Next.js 确实为开发人员执行了自动代码分割。

对于营销人员来说，改进后的 SEO 非常棒。对于企业主来说，由于 Next.js 中的许多预制组件，网站和应用程序的更快上市时间成为可能。此外，因为 Next.js 有助于制作静态网站，所以安全性得到了提高；也没有与数据库或用户数据的连接。

# Next.js 的优缺点

**优势**

*   在加载时间方面表现出色
*   加载时间有助于“延迟加载”和自动代码分割
*   对开发者的大量支持
*   奇妙的用户体验
*   更快上市

**next . js 的缺点有**

*   一些开发者认为它太固执己见了
*   许多开发者抱怨 Next.js 的路由方式，其他人则支持它

# 结论

你试过 Next.js 吗？

嗯，你今天可以在 [Fathym 平台上免费！](https://www.fathym.com/dashboard)

如果有，也许你想和其他框架一起评估 Next.js，比如 React、Angular 或 Svelte。

或者，用 Next.js 为一条路线——也许是你的主页——创建一个应用程序，然后在它旁边使用无代码工具为另一条路线——也许是博客——创建一个应用程序？开发者的选择是无限的，所以今天就选择你自己的旅程吧。

【https://www.fathym.com】最初发表于[](https://www.fathym.com/blog/articles/2022/september/2022-09-07-positives-and-negatives-of-nextjs)**。**

**更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。****