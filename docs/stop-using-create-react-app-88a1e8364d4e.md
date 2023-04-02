# 停止使用 Create React App！

> 原文：<https://javascript.plainenglish.io/stop-using-create-react-app-88a1e8364d4e?source=collection_archive---------1----------------------->

## 相反，使用支持您构建现代前端的工具包。

![](img/487a5716cca50990844ab4b95d6b9064.png)

Photo by [Piotr Musioł](https://unsplash.com/@szamanm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您已经使用 Create React 应用程序一段时间了，并且最终开始对它感到舒适，那么是时候离开并看看这个世界还能提供什么了！不，我不是在谈论研究其他 JavaScript 库或框架。特别是当你是初学者时，我会建议你坚持使用一个库，直到你**不得不**切换。

Create React App 附带了几个预定义的工具和预设，可能没有你想象的那么有益。例如，构建 SSR 应用程序是一项相对棘手的任务。此外，CRA 正在开发 Webpack，这很可能达到了它的目的。还有其他构建工具，它们不仅速度更快，而且基于其他技术基础。如果你不想落后，我建议你切换到另一个工具链。

我遇到过一些 React 开发人员，他们从未在没有创建 React 应用的情况下编写过 React 应用。所以他们很难看到工具链能够并且应该提供什么。CRA 也有一些好的东西；例如，它附带了一个测试设置，与其他解决方案相比，在如何构建应用程序方面，它给了你很大的自由度。然而，当涉及到扩展时，它有点剥夺了这种自由度，因为您要么必须退出，要么必须引入另一个库来扩展 CRAs 的 Webpack 配置。

让我们看看 CRA 的选择；你能用什么，又何必多此一举？

## NextJS

NextJS 可能是除了 CRA 之外最流行的工具链。它有自己的路由和样式解决方案(在使用 SSR 时，样式可能很复杂)。NextJS 的维护者 Vercel 也负责其他可以在任何 React 项目中使用的包(比如 swr)。因此，他们在某种程度上积极地为 React 宇宙做贡献，这是我喜欢的。

NextJS 应用可以部署到 Vercel 自己的平台上(非商业网站免费)。我最后一次尝试时，它是一个简单的过程，允许任何人立即部署他们的应用程序。

除了 React 提供的您所了解和喜爱的一切，NextJS 还使用自己的 API 来简化 SSR 和后端开发——甚至对于前端开发人员也是如此。

有了 React18 和 HTTP3，我期待网站更多地使用流媒体，因此这将是未来令人兴奋的候选。

如果一个健壮的、经得起未来考验的库是你正在寻找的:别再找了。现在就学习 next js:【https://nextjs.org/learn】T4

如果您已经尝试过 NextJS，但它离 React 太远，无法理解，或者您只是不喜欢这个 API，请继续阅读！会很有趣的。

## 再搅拌

Remix 拥有 NextJS 拥有的一切。他们正在为 React 生态系统(React-Router 的制造商)做出贡献，使用 React 开发 SSR 应用变得轻而易举，但有一个巨大的不同:他们对扩展更加开放，更接近 React 的 API。至少，这是我不得不与 Remix 和 NextJS 合作时的印象。我还觉得 Remix 更快，在 Remix 的环境中写 React 时，我感觉更“自在”。

我认为 Remix 是更好的 NextJS，我会在我的下一个项目中使用它。如果您考虑使用它，那么您也应该意识到它的缺点:

*   社区没有 NextJS 的社区大。
*   混音可能不是一个好名字；很难从谷歌上获得建议(尽管你可能会在“RemixJS”上获得成功)。
*   目前使用 Remix 的项目并不多。

有些起伏可能只是我的经历，你的可能不同。意识到这一点。

要了解 Remix 以及如何使用它创建你的下一个 React 应用，从这里开始:[https://remix.run/docs/en/v1](https://remix.run/docs/en/v1)

## 其他 React 工具链和创建自己的工具链

还有许多我没有提到的其他 React 工具链。主要是因为我用的不多。对于初学者来说，React 文档可能是一个很好的起点，因为它引出了一些备选方案【https://reactjs.org/docs/create-a-new-react-app.html[】。你会注意到当前的文档甚至没有提到 Remix。不过即将发布的 doc 会这么做:](https://reactjs.org/docs/create-a-new-react-app.html)[https://beta . react js . org/learn/start-a-new-react-project # popular-alternatives](https://beta.reactjs.org/learn/start-a-new-react-project#popular-alternatives)。

此外，我不想在定制工具链上丢失很多单词；我只想说:不要！创建合适的工具链需要大量的工作。有教程教你如何向现有的工具链添加任何东西，比如 Remix，NextJS，甚至 CRA。向它们添加诸如 Tailwind、Jest 或 Storybook 之类的东西相对简单，而手动设置它们(尤其是结合 TypeScript)可能是一场噩梦。相反，找到一个最适合你的工具链——我相信这意味着停止使用 Create React App。

就这些了，伙计们。非常感谢你的来访。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*