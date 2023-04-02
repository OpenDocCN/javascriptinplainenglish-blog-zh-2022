# 是时候抛弃 Firebase 了——开始使用 Next.js

> 原文：<https://javascript.plainenglish.io/time-to-ditch-firebase-for-good-start-using-next-js-79a29aa84a9?source=collection_archive---------7----------------------->

## Firebase 不再可行了吗？

![](img/1997fb7d1be1090b6a7f15ebc4f63f48.png)

Credits: [Pixabay](https://www.pexels.com/sk-sk/@pixabay?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) on [Pexels](https://www.pexels.com/sk-sk/fotka/kvet-semena-farby-hracka-434163/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

最近发了一篇关于再也不用 Firebase 的帖子。在这篇文章中，我提到了一个仍然让我联想到 Firebase 的链接。这是建立在 Firebase 之上的产品，叫做 [Deap Market](https://deapmarket.com/) 。

Deap Market 是我前段时间创作的一个产品，并没有真正获得多少荣耀。然而，我还没有完全放弃这个项目。我决定呼吸一些新鲜空气。

**我的计划是做 3 件重要的事情:**

*   *从客户端渲染切换到服务器端渲染*
*   *用 Vercel* [*边缘函数*](https://vercel.com/docs/concepts/functions/edge-functions) *代替* [*Firebase 函数*](https://firebase.google.com/products/functions)
*   彻底反思商业模式

在这个故事中，我将谈论前 2 点，以及为什么我认为它们对该产品的成功至关重要。我将分享我对 Firebase 及其可行性的看法。我还将分享我从 Firebase 迁移到 NextJS 的经验。

但是首先，**让我解释一下我为什么首先使用 Firebase。**

# 初学者的错误

那是一个周日的早晨，我突然想到一个主意，*“让我们创造一个产生内容想法的工具。”这不是什么新发现。事实上，市场上已经有类似的网站。然而，我发现它们都定价过高，不值我的钱。*

![](img/6894d86d224628f74cfb8607e589437e.png)

Credits: [Anete Lusina](https://www.pexels.com/sk-sk/@anete-lusina?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) on [Pexels](https://www.pexels.com/sk-sk/fotka/inspiracia-sebaisty-napad-apartman-4792509/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

我想创造一种更实惠的工具，为客户带来更多价值。我打开 VS Code，马上开始编码。没有设计，没有执行计划，只有纯粹的意志力去创造令人兴奋的东西。

一两个月后，产品就可以投放市场了。几个星期后，在广告上花了几百美元，我意识到一些不那么令人愉快的事情。

## 搜索引擎优化的问题

没有办法通过搜索引擎有机地到达网站。当然，SEO 需要时间，大家都知道。但是如果你的网站是在客户端呈现的话，要提高 SEO 是相当困难的。

我吸取了教训，这些天，我总是在开始一个项目之前问自己一个问题，*“这个网站需要 SEO 优化吗？”如果你是一名网络开发人员，你应该在写一行代码之前问自己同样的问题。*

## 无服务器功能的问题

起初，我非常喜欢 Firebase 的无服务器功能。我不需要设置任何服务器，但是我可以使用外部服务。起初一切似乎都正常，但当我尝试我的应用程序的部署版本时，我有点失望。

无服务器功能的问题是它们冷启动。如果函数本身在一段时间内没有活动，那么它的执行会花费很多时间。这降低了性能，尤其是当网站没有这么多活跃用户的时候。

# 开关

在评估了我的情况后，这种转变似乎是一个急需的选择。毕竟，NextJS 使用的是服务器端渲染，这对于 SEO 来说要好得多。最重要的是，我可以使用 Vercel 的 Edge 函数实现零冷启动。

你可能已经猜到了，对我来说，转型是一个显而易见的选择。我有点害怕这个转变。这看起来像是很多工作，但实际上，只花了我一天的时间。然而，这实际上取决于代码库的大小和依赖项的数量。对我来说，没有。

我完成了迁移，我对应用程序的性能非常满意。我也很高兴它被呈现在服务器上。为建设 SEO 打下良好的基础。这肯定会是一场艰苦的战斗，但至少我们有所作为。

如果你对这个网站很好奇，想去看看，你可以点击[这个链接](https://deapmarket.com/)去看看。

![](img/b6fc939b0896ed4c61ded815854ef167.png)

[Deap Market | Homepage](https://deapmarket.com/)

最后一座把我和火焰基地联系在一起的桥现在被烧毁了。在这一点上，我很有信心我不会将它用于我将来要构建的任何 web 应用程序。

我仍然看到 Firebase 的好应用程序，其中一个是移动应用程序开发。但是就 Web 开发而言，不，谢谢！

# 从这里我们能得到什么

我和 Firebase 肯定有过一段美好的时光，但那都是过去的事了。截至今天，我完成了将 [Deap Market](https://deapmarket.com/) 移植到 Vercel 生态系统中，这意味着我正在将代码库重写到 NextJS 框架中。

整个过程很顺利，尽管我最初很稀缺。但是有一件事更重要。如果我不先进入实现阶段，所有这些步骤都可以避免。

我相信这是我经验中的关键。如果你正在开发一个产品，不要只考虑代码。

**想想你的顾客，想想你的营销，想想你将如何交付你的产品。**

这些重要的问题总是需要先回答的。只有在它们之后，才应该选择科技堆叠，记住它们。现在我只有一个问题要问你。

***开始编码前有没有思考分析？***

我希望你喜欢这个故事。如果你想从我这里听到更多或阅读更多，可以考虑通过使用 [***这个链接***](https://bernardbad.medium.com/membership) ***成为一名中等会员。***

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***