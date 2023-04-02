# React 上下文 API:功能组件简介及使用方法

> 原文：<https://javascript.plainenglish.io/react-context-api-introduction-and-how-to-use-in-the-functional-component-e01dcd8388a1?source=collection_archive---------1----------------------->

## 上下文 API 解决了什么问题？**React 中的上下文 API 是什么？我们如何在功能组件中使用上下文？**

![](img/802d0cc93c06e1091e96874bd5432ffe.png)

Photo by [Malte Helmhold](https://unsplash.com/@maltehelmhold?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这个博客分为多个部分。首先，我们将看到背景，并理解**上下文解决什么问题。**然后其次，我们将看到**React 中的上下文 API 是什么。**最后，**我们如何在功能组件中使用上下文。**

# 道具和组件之间的通信:

我们都知道，我们使用 props 将数据从父组件传递到子组件，这也被称为**单向数据流**。

但是，如果我们有多个嵌套组件，从父组件到最后一个子组件可能需要数据，而中间的其他组件不需要数据，那么传递属性就会变得冗长和不方便。我们仍然需要将道具从顶级父组件传递到所有中间组件，并最终到达最后一个子组件。

让我们通过下面的例子来看看这一点:

在上面的代码片段中，我们有一个顶级的" **App** "组件，其中的" **products** "数据作为 **prop** 传递给" **ProductLayout** "组件，并进一步向下传递给" **Product** "和" **Card** "组件。

“ **ProductLayout** 组件真的需要**产品**数据作为**道具**吗？

答案是一个大大的不！

只有“ **Product** ”组件需要这些数据，但是由于我们有一个嵌套组件，react 允许您将数据作为道具从父组件传递到子组件。所以我们就遇到了这种情况。

# 什么是道具打钻，道具有问题？

![](img/8e59b1e08740611d08d7ef8a63ebbd1a.png)

Photo by [Daniel Smyth](https://unsplash.com/@smudgern6?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

虽然，props 是通过 UI 树向使用它的组件传递数据的一种很好的方式，但是当你的 react 应用程序有深度嵌套的组件，并且许多组件之间(像上面例子中的<productlayout>)不需要传递 props，但我们仍然传递它，这很快就会变得不方便和复杂。这种情况称为支柱钻孔。</productlayout>

# 什么是上下文 API？

**上下文 api 允许您将数据从父组件传递到使用它的子组件，而无需通过 props 将数据显式传递到中间的每个子组件。这就是如何通过避免钻牛角尖来编写更干净的代码。这也被认为是一种较轻的状态管理方法。**

# react 中的 useContext 是什么？

![](img/624e3c8943901024a2abcee88a6e4f3a.png)

Photo by [James Wheeler](https://unsplash.com/@souvenirpixels?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

useContext 是一个 React 钩子，让你在功能组件中使用上下文 api。

## **在应用中使用上下文有三个步骤:**

1.  *在父组件中创建上下文。*
2.  *使用您创建的上下文进行包装，并将数据传递给需要它的子组件。*
3.  *消费子组件中的数据。*

## 让我们在上面的代码片段中使用上下文

现在，与之前的 prop drilling(没有上下文)相比，在上下文的帮助下，代码片段更加干净和可维护。

# 结论:

1.  React 上下文 API 可以帮助您避免钻取错误，并使您代码更加整洁。
2.  上下文为您的 web 应用程序提供了一种更简单的状态管理方法。

**注意:**不代表 context API 可以代替 Redux。这只是一种较轻的方法。在管理大型 web 应用程序时，Redux 有自己的用例。

如果你想要更多这样的内容，请在媒体上关注我，并订阅我的 YouTube 频道。

你也可以在推特上找到我。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。***