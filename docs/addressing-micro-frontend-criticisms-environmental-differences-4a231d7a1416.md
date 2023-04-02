# 解决微观前端批评和环境差异

> 原文：<https://javascript.plainenglish.io/addressing-micro-frontend-criticisms-environmental-differences-4a231d7a1416?source=collection_archive---------17----------------------->

## 如何正确使用微前端

![](img/20d42cb31e8cc70b07a7179c6e2fffcc.png)

微前端是未来的趋势，是网站前端开发的下一件大事。但是，这只是在你正确使用它们的情况下。

当然，微前端并不完美，它们也有一些负面的内涵。这就是我们希望澄清的地方，并解释我们如何使用不同于其他人的前端架构。

首先，[我们完全模块化的方法](https://www.fathym.com/blog/articles/2022/june/2022-06-06-go-fully-modular-frontend)意味着每个页面(或路线)由一个独立的团队管理。我们没有多个团队将他们的工作合并到一个页面或容器中，就像早期定义的微前端一样。但稍后会详细介绍。

现在，让我们定义一下微前端。

# 定义

从本质上来说，[微前端](https://www.fathym.com/blog/articles/2022/march/2022-03-14-a-simple-micro-frontends-explainer)仅仅意味着把一个单一的前端——刚性的、不可移动的、不可分割的——分解成更小的部分。这些较小的部分然后由小团队处理，小团队朝着共同的目标自主工作。

使用微前端的好处有很多。人们可以将较大的代码库分解成较小的部分，这意味着更快的构建和修复。可以在站点的一部分执行更新，而不需要整个站点停机。此外，多个不同的 [JavaScript 框架](https://www.fathym.com/blog/articles/2022/april/2022-04-21-four-javascript-frameworks-you-should-know)可以在一个项目中使用。

![](img/52ad70223476ce14d8a95ce92fb3d22f.png)

在这个例子中，主页是在 React 中构建的，React 是目前最流行的框架之一。论坛创建于 Angular。同时，博客是用 Svelte 创建的，静态站点生成器 Docusaurus 运行技术文档。

除了能够使用这些不同的框架之外，想象每一条路由都是由不同的团队(或个人)构建和维护的。这又使得网站的某个方面的更新变得更容易、更快，因为每个团队不一定要等另一个团队完成后才能更新。

微前端也意味着更小的代码库，这意味着更快的错误修复和更快的整体构建。

## 何时使用它们

真的，使用微前端没有什么不好的时候。对于一个小团队或个人表演来说，这似乎没有必要，但关注未来也是有意义的。因为如果一个团队的规模扩大了，其他人可以加入进来，并被赋予特定的任务或目标。

在一个网站上工作的团队越大，将工作量分成更小的、可以由更小的团队管理的小块就越有意义。如果你在一个页面上有一个 bug 或错误发生，不一定会影响到其他页面。这意味着您可以在网站的其余部分仍然正常运行的情况下解决这个问题。

## 环境差异批评

当我们致力于支持微前端时，我们也在研究 Martin Fowler 对架构的批评。

在之前的博客中，[我们提到了他们对有效载荷大小的批评。](https://www.fathym.com/blog/articles/2022/march/2022-03-31-addressing-micro-frontend-criticisms-payload)是的，这是真的，用 React 的多次迭代构建整个站点可能会降低性能。但是，在可能和适用的情况下，我们希望使用静态站点生成器和轻量级 JavaScript 框架——如 Svelte 和 Vue。(在上面发布的链接中阅读更多信息。)

现在，转到环境差异，马丁·福勒 2019 年的博客将其解释为:

“如果我们在不像生产的环境中进行本地开发，我们需要确保我们定期将我们的微前端集成和部署到像生产的环境中，并且我们应该在这些环境中进行测试(手动和自动)以尽早发现集成问题。”

## 解决办法

我们有两种不同的方法来解决这个问题。

首先，由于微前端的新的和改进的版本/定义——我们认为它是完全模块化的(链接)——每个前端都托管在它自己的路由上。因此，不存在共享容器，这是考虑微前端的旧方式，也不存在集成问题。

例如，如果你的主页是用 React(【www.yoursite.com】)创建的，而你的论坛是用 Angular(【www.yoursite.com/forum】)创建的，那么它们是不同的存储库，托管在不同的路径上，由不同的团队管理。尽管它们似乎运行在同一个域中，但它们是完全模块化的，彼此独立，因此不存在集成问题。

![](img/8962325e5019fb41dc25fc12836dda63.png)

其次，我们通过在 Fathym 中设置测试路径来避免这些环境差异，这些测试路径托管您的/feature 分支，QA 团队可以在将它合并到集成之前验证它是否工作。这意味着创建一个类似于生产的环境，并在部署之前进行测试，因此要知道它会起作用。

“当你把它推向生活，没有什么是惊喜。这是一个很大的效率增益，”工程总监杰里米·汤姆林森解释说。“Fathym 帮助您取得成功，并消除这些令人头痛的问题，因此开发人员不能只是猜测。”

我们的目标不仅是降低建立网站所需的开发经验的门槛，而且是尽早发现集成问题。"

[我们邀请你现在就注册 Fathym，](https://www.fathym.com/dashboard)这不仅是为了实现你的目标，也是为了从中获得一点乐趣。

*最初发表于*[T5【https://www.fathym.com】](https://www.fathym.com/blog/articles/2022/june/2022-06-09-micro-frontend-criticisms-environmental-differences)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***