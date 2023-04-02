# 如何在 Next.js 中使用环境变量

> 原文：<https://javascript.plainenglish.io/how-to-use-environment-variables-in-next-js-353824614686?source=collection_archive---------2----------------------->

## 看看如何在 Next.js 中使用环境变量。

![](img/9e8a22d27ca1885731aad5aa1ec8abae.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

next . js——这个名字对于任何使用 React 的开发人员来说都不陌生。由于有多条路线，水疗中心的发展变得很容易。由于其服务器端渲染方法，它也有助于搜索引擎优化。

作为开发者，Next.js 通过在引擎盖下做繁重的工作，为我们提供了许多特性。在 Next.js 提供给我们的众多特性中，我个人最喜欢的一个是对环境变量的*内置支持。*

环境变量是存储应用程序敏感信息的好方法。API 键和数据库密码是作为环境变量存储得最多的值，但是您可以存储任何东西。

整个应用程序都可以访问这些变量，它们不会暴露给浏览器，只存储在服务器上。这就是环境变量如此特殊的原因。

因为 Next.js 为我们提供了内置支持，所以我们不必依赖外部包来使用项目中的环境变量。

要在 Next.js 项目中使用环境变量，请在项目目录的根目录下创建一个名为`.env.local`的文件。我们可以在这个文件中存储与我们的应用程序相关的所有敏感值。

`.env.local`内的变量:

```
// inside '.env.local' file
NAME=test123
```

这里，我们有一个名为“NAME”的变量，其值为“test123”。如你所见，‘test 123’是一个字符串，但是我们没有把它存储在单引号或双引号中。

我们在这个文件中创建的所有变量都以这种格式存储。

Next.js 环境变量的默认行为是这些变量只能在 Node.js 环境中访问。

> *“getStaticProps”*和*“getServerSideProps”*是 Next.js 提供给我们的两个方法，它们给了我们一个 Node.js 环境，有助于数据抓取和服务器端渲染。如果你不知道这些方法，我推荐你在这里阅读它们，以便更好地理解这篇文章。

这两个函数都支持节点`process`模型，这是一个全局对象，意味着它可以在不使用“require”的情况下使用。在这些函数中，您可以编写常规的 Node.js 代码。因为这些函数支持 Node.js，所以可以使用“process.env”来访问环境变量。

最后，这些函数返回一个对象，这个对象有一个“道具”键，这个键也是一个对象，这个对象包含了我们在应用程序中想要使用的所有道具。

看看下面的例子:

```
// pages/index.js (inside the pages directory, rendering "index.js")
export default function Home(props) {return <h1>{props.secret}</h1>;}function getStaticProps() {
 return {
  props: {
   secret: props.env.NAME
  }
 }
}
```

这里，当我们请求" index.js "页面时， **"getStaticProps "将在" Home "功能组件**之前首先运行，返回" Props "对象，该对象将保存一个名为" secret "的道具，其值是我们从前面设置的环境变量中获取的。

这个函数完成后，我们可以访问“Home”组件中的“秘密”道具。这样，我们的秘密仍然安全，我们的应用程序也像以前一样工作。

我建议学习更多关于 getStaticProps 和 getServerSide props 的知识，因为它们可以做更多的事情，而不仅仅是帮助处理环境变量。看看他们的官方文件[这里](https://nextjs.org/docs/basic-features/data-fetching/get-static-props)。

# 结论:

对于 React 来说，Next.js 是一个非常令人印象深刻的框架，可以用来制作一个生产就绪的应用程序。它不仅提供了环境变量，还提供了更多。你可以在这里看看他们的官方文件[。](https://nextjs.org/)

作为一名开发人员，有时会需要将一些信息存储在不对最终用户公开的地方，使用环境变量有助于我们实现这一点。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*