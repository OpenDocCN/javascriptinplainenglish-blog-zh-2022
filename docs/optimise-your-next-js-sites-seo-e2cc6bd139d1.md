# 优化你的 Next.js 网站的搜索引擎优化

> 原文：<https://javascript.plainenglish.io/optimise-your-next-js-sites-seo-e2cc6bd139d1?source=collection_archive---------13----------------------->

当建立一个网站时，你可能已经有了一个清晰的目标。尽可能快地让它登上排行榜的首位。为了实现这个目标，你可以付费做广告，或者做个聪明人，在 SEO 上花些时间。相信我，最后一条从长远来看是值得的！

在这篇文章中，你将学到一些技巧和窍门，如何优化你的 Next.js 站点，使其在 Google 和 Bing 这样的搜索引擎中排名靠前！

![](img/0689620fa87ae3fe884f13e28e7a3aec.png)

Image by [Merakist](https://unsplash.com/@merakist)

# 设置正确的标签

当建立一个网站时，你很可能遇到过著名的元标签。由于它们有数百个名称和变体，很容易忘记一些。幸运的是，有一个非常方便的包，可以很容易地将这些标签添加到我们的 Next.js 站点中！

看看加里·米恩的下一部 SEO 。这个包为你提供了一个 React 组件，使得在页面到页面或者全局的基础上设置你所有的 SEO 标签变得非常容易。

Example from the Next-SEO documentation

正如你在上面的例子中看到的，Next-SEO 为你提供了所有你需要的工具，从经典的元标题和描述到 Twitter 卡片和开放图表模式！

对于 TypeScript 用户来说，Next-SEO 带有内置类型，这意味着它可以很容易地向您显示您必须配置的所有选项！

# 使用服务器端呈现或静态生成

当使用像 React 这样的前端框架或库时，你很快就会发现客户端渲染并不完美。虽然它可能很快，但对 SEO 是有害的，因为来自 Google 和 Bing 的爬虫不能读取你页面的内容。

幸运的是，Next.js 让服务器端呈现页面变得非常容易。服务器端呈现意味着 HTML 及其内容一旦加载就完全可用。页面上没有仍在获取数据的骨架或微调器。

Example from the Next.JS documentation

## 更好的是，静态生成

不过，服务器端渲染确实有一个缺点。这相当耗费资源，当你试图扩展你的网站时，你会很快发现你的服务器很难满足所有的请求。

这就是静态生成发挥作用的地方。静态生成的页面是在构建应用程序时构建的。这意味着他们的 HTML 已经在应用程序中准备好了，只需要提供给用户。不需要调用服务器来获取数据。

在我的应用程序[on board](https://www.onboarded.app/)中可以找到静态生成的真实例子。在这个平台上，所有的公司和职位页面都是预先构建的，因为数据在构建时就已经可用了！这不仅是伟大的搜索引擎优化，但它也使他们真的很快！

Example from the Next.JS documentation

# 保持内容新鲜

SEO 最重要的部分之一是保持你的内容新鲜。您可以通过多种方式做到这一点。

*   添加新内容，在页面上添加新部分，或者创建全新的页面，如博客文章
*   更新过时的内容，内容可能会过时，请确保所有内容都是最新的

确保你的内容有价值，人们在点击离开之前花在你网站上的时间对搜索引擎优化非常重要。搜索引擎只有一个目的，那就是为你的查询提供最好的网站。如果你搜索一个查询，点击顶部的链接，并立即退出，那么搜索引擎将跟踪这一点，并为该网站提供更少的给定查询。

祝你有一流的一天！💜

你听说过程序化 SEO 吗？在 https://launchman.io/了解更多信息

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***