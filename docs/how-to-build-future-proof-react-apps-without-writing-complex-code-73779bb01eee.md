# 如何在不编写复杂代码的情况下构建面向未来的 React 应用

> 原文：<https://javascript.plainenglish.io/how-to-build-future-proof-react-apps-without-writing-complex-code-73779bb01eee?source=collection_archive---------7----------------------->

## 这些简单的提示将帮助您构建非常容易测试、更新和超级灵活的 React 应用程序。

![](img/48031dffffd19a1c2b35f12fff746011.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写伟大的代码并不复杂。这些简单的提示将帮助您构建非常容易测试、更新和超级灵活的 React 应用程序。

不幸的是，我们经常在构建应用程序时没有考虑它们将如何演变以适应未来的变化。

## 这些技术将如何成为救命稻草

以下是一些常见的场景，在这些场景中，这些小技巧将被证明是救命稻草:

*   容易测试。
*   适应未来的更新。
*   业务逻辑的分离。
*   可预测的数据流。

## **编写面向未来的组件**

编写组件时，请始终记住这些经验法则:

*   UI 组件应该总是不知道网络请求、业务逻辑或应用程序状态。
*   **组件应该像纯函数一样编写。**它仅仅意味着当提供相同的道具时，它应该总是渲染相同的数据。
*   获取编写优秀组件的详细指南。[查看本指南](https://blog.bitsrc.io/5-steps-to-build-react-components-like-a-pro-fb1f3af6ba17)。

## **使用 hoc 简化进化**

反应高阶组件(HOC)是一个接受一个组件并返回一个组件的组件。

编写 HOC 时，请始终记住这些经验法则:

*   总是喜欢创造那些不创造任何道具的 hoc。如果您的 HOC 需要创建道具，请确保它不会创建多个道具。
*   当该行为由应用程序中的多个组件或所有组件使用时，请使用 HOC。
*   确保组件可以在没有 HOC 的情况下工作。组件不应创建与 HOC 的依赖关系。
*   组件可以直接包装在 HOC 中，而不必添加额外的逻辑。

## **为干净的代码构建您的应用**

不要在一个地方混合视图渲染、数据处理和数据获取。把什么都混在一起，会导致意大利面条式的架构，将来会变得痛苦。

总是让你的组件尽可能的笨。给定相同的状态，组件应该总是呈现相同的东西。

Flux 架构允许您为应用程序创建可预测的数据流。在这个架构事件中，监听器监听诸如用户输入处理程序和网络请求处理程序之类的东西。当事件侦听器获得它们时，它会将操作分派给存储。状态仅在调度操作时更新。

使用基于 flux 架构的库，如 Reflux、Redux 等。在以下场景中:

*   该组件使用网络请求或设备 API。
*   具有通用的应用程序状态。
*   该组件需要与应用程序的其他部分共享的业务逻辑或数据操作逻辑。

使用 flux architecture 不仅可以让你构建高度灵活的 UI 组件，还可以让你将业务逻辑之类的东西从组件中分离出来。它将允许您轻松地迁移到不同的数据获取技术。可预测的单向数据流将使您的应用程序易于调试和测试。

把 reducers 想象成你的应用程序的核心，把 dispatchers 想象成适配器。不要在组件中混合业务逻辑，而是将它们放在 Redux(或您正在使用的任何东西)中，并用动作创建器触发状态变化。

在我的[*types share 社交博客*](https://typeshare.co/amit08255/posts/template-2-how-to-guide-yqvd) *上阅读这篇文章和更多内容。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***