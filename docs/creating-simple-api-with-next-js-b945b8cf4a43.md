# 如何用 Next.js 创建简单的 API

> 原文：<https://javascript.plainenglish.io/creating-simple-api-with-next-js-b945b8cf4a43?source=collection_archive---------9----------------------->

## 使用 Next.js 创建简单 API 的指南

![](img/871f4b405d2bfa227da36b38f7b3c2d7.png)

Photo by [Rames Quinerie](https://unsplash.com/@ramesquinerie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你已经熟悉 React，你可能听说过 Next.js。它是由 Vercel 构建的 React 框架。它为我们提供了一条开箱即用的可选路径，这意味着我们可以用 JavaScript 编写后端代码。所以让我们开始创建我们的第一个 API。

## 安装 Next.js

在您的终端中运行以下命令:

```
npx create-next-app@latest
```

安装完成后，您会看到一些来自 Next.js 的样板文件。现在只需关注`pages`文件夹。默认情况下，里面会有`api`文件夹、`_app.js`和`index.js`文件。`Index.js`文件就像我们的 home 组件，`_app.js`是我们应用程序的包装器，`api`文件夹是我们将要创建的 API 的所有端点所在的地方。

不要忘记运行下面的命令来启动我们的下一个应用程序:

```
npm run dev
```

这个命令将在 http://localhost:3000 启动我们的应用程序。

现在让我们只关注`api`文件夹，因为我们的工作主要在这里。在`api`文件夹里，你会看到`hello.js`文件，如果你愿意，你可以删除它。

在这个演示中，假设我们想要制作一个 API，它将返回一个英雄和角色的集合。在 Next.js 中，我们的文件夹结构将成为我们的端点路径，因此我们将更容易组织它。

现在创建`heroes`文件夹，并在其中创建一个`index.js`文件。如果 URL 中没有发送参数，`index.js`文件将成为默认路径。由于我们也想获得具有特定 id 的英雄，所以我们也在英雄文件夹中创建了`[id].js`文件。为了在 Next.js 中创建一个动态 API 路由，我们必须将文件名放在括号中，以告诉 Next.js 这是一个动态路由。在`index.js`文件中，编写如下所示的代码:

```
export default async function handler(req, res) {let data = await fetch(`${urlToFetch}`)let json = await data.json()res.send(json)}
```

这段代码将检索所有英雄的列表，并将其发送回客户端*(注意:您可以根据需要修改代码)。*

要访问我们的 API，我们需要追加我们的 URL。我们的 URL 变成了[*http://localhost:3000*](http://localhost:3000)*/API/heroes*，因为我们在 heroes 文件夹中，我们需要在 URL 中反映它。

现在在`[id].js`文件中，编写如下所示的代码:

```
export default async function handler(req, res) {let id = req.query.idlet data = await fetch(`${urlToFetch}/${id}`)let json = await data.json()res.send(json)}
```

要访问 API，我们只需要编写[*http://localhost:3000*](http://localhost:3000)*/API/heroes/{ id }*并用某个特定的 id 替换 id 即可。注意，我们可以使用与文件名相同的单词来访问 URL 中的参数，因为我们的文件名是`[id].js`，那么我们就可以得到它`by req.query.id`。这将向客户端发送包含特定数据的响应。角色部分也是如此，我们只需要在英雄文件夹的同一层再创建一个文件夹。

就是这样！希望这篇文章能帮助你开始用 Next.js 创建 API，干杯！🍻

## 进一步阅读

[](/data-fetching-with-next-js-13s-bleeding-edge-features-a-primer-a60ddd3f7570) [## 使用 Next.js 13 的前沿特性获取数据——入门

### NextJS 13 中的数据获取使用了应用程序目录、流、暂挂以及混合服务器和客户端组件。

javascript.plainenglish.io](/data-fetching-with-next-js-13s-bleeding-edge-features-a-primer-a60ddd3f7570) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***