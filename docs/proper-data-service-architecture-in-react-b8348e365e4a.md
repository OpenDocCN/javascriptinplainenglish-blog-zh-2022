# React 中合适的数据服务架构

> 原文：<https://javascript.plainenglish.io/proper-data-service-architecture-in-react-b8348e365e4a?source=collection_archive---------5----------------------->

## 如何为 React 世界中的变化做好准备

![](img/24e93f9d7976c9cae824a224e892a07a.png)

Photo by [Ryan Quintal](https://unsplash.com/@ryanquintal?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/building-blocks?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

很多时候，开发人员努力构建合适的数据服务。一开始，我们得到了 React 类服务→它很快过渡到 Redux 和 Sagas，以轻松处理副作用并对加载状态变化做出“反应”,但在学习和理解生命周期中发生的事情时，它变得势不可挡，然后 hooks 通过 magic useEffect()进入游戏，当我们开始使用它时，像 [React Query](https://react-query.tanstack.com/) 这样新的更智能的库出现了。我们如何为 React world 中的这些变化准备我们的应用程序？我们能做到既便宜又安全，不需要重写一半的代码库吗？在这篇文章中，我将向您展示一个简单的方法，如何为变化做好准备。

# 耦合问题

先说耦合问题。我这么说是什么意思？上述所有问题都来自于对所提到的库的错误使用。我并不是说这些技术中的任何一种是好的或坏的，可能所有这些技术在某一点上都是好的，真正的问题是这些库的使用！我知道，我知道……每个人都在阅读文档并尽力而为，但真正的问题是这些技术被直接用于应用程序——这归结为耦合问题。

让我们来看一个将 Redux Saga 重写为 ReactQuery 的例子，我们有这样的代码:

你可以想象你有多少地方和额外的 reducer，actions，和 sagas 文件。所以现在你需要重构它——如果所有的代码都是像这样创建的——我们总是有`data`，`loading`,它是通过`useSelector`直接从状态中获取的。我们可以开始认为它是非常通用的，我们可以编写一些 codemod 来更新它以实现一种新的数据服务方式(例如 React Query)。但是我们都知道现实是不同的，一些开发者自己做了一些选择，例如`useSelector(selectFunction)`等等。所有这些情况对于 codemods 来说都变得太复杂了，所以我们最终只能手动重写所有的地方。所以我们需要做的是把这段代码改成:

当我们检查完所有的文件，最终进行重构的时候，我们就可以开香槟庆祝了(当然前提是我们的老板不会问我们为什么在一些看不见的重构上花了很多时间)。但是后来……React Query 改变了他们的 API，现在`useQuery` hook 返回一个数组，而不是一个对象，例如`[data, loading, error]`——好吧，这并不坏，我们仍然可以创建 codemod，当然在这之前我们需要向我们的老板解释，并要求时间进行更新，因为我们所有人都想使用更新的库。但是我们都知道 JS 世界的变化有多快，所以我们可以假设新的“超级酷”库会出现。然后我们需要再次去找我们的老板…

![](img/934efdddc1c3003353244430484a803c.png)

求时间重构。

# 解决办法

也许你能想到一个解决办法，我有一个非常简单的办法——让我们创建自己的 API 并抽象出库。这么简单对吧？让我们想象一下，如果我们有一个带有全公司 API 的服务挂钩包，那么重构会有多简单？让我们在示例中这样做，并让我们将 Redux 代码转换为自定义服务挂钩:

将这个逻辑移到一个单独的钩子上非常重要，更重要的是始终保持相同的输出形状——因为这将节省我们很多时间，让我们在组件中使用它:

现在，我们想从 Redux 迁移到 React Query，你可以看到我们可以很容易地做到这一点，因为我们唯一需要改变的是我们的服务挂钩:

而且组件看起来也是一样的，没有必要对组件做改动！唯一需要改变的是我们的服务挂钩。

正如您所看到的，这真的很酷，因为无论 React Query API 是否会改变，或者我们是否希望从一种技术迁移到另一种技术，我们都只有一层需要测试和重写。此外，你可以想象一个团队交付服务，第二个团队只是从服务库中使用它，这真的很容易，因为我们总是知道我们将拥有什么 API，从开发人员的角度来看，我们不在乎在引擎盖下使用什么——是 React Query，Redux Saga，还是完全不同的东西。

# 摘要

我向您展示了代码迁移问题的一个非常简单的解决方案——我们都知道，有时候抽象可能会让人不知所措，而且要明确的是，它并不是适用于所有情况的模式。创建一个服务挂钩包并公开一个 API 是一个经过充分测试的模式(重要的是，这个 API 应该像我们的合同一样，不应该改变)。由于这一点，我们只有一层要测试，我们可以将整个公司的爆炸半径降至最低。

你可以在[推特](https://twitter.com/novakPe_)上关注我，感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*