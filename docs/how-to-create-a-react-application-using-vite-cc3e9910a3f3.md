# 如何使用 Vite 创建一个 React 应用程序

> 原文：<https://javascript.plainenglish.io/how-to-create-a-react-application-using-vite-cc3e9910a3f3?source=collection_archive---------5----------------------->

## 开发 React 应用程序时节省时间

![](img/ebbdb1362f54406547266ddb3d31ebae.png)

Photo by Cup of Couple: [https://www.pexels.com/photo/modern-workplace-with-computer-and-notepad-6177557/](https://www.pexels.com/photo/modern-workplace-with-computer-and-notepad-6177557/)

你可以用很多方法创建一个 [*React*](https://github.com/facebook/react) 应用，比如使用 [*创建 React App*](https://github.com/facebook/create-react-app) (CRA)。反动派和 CRA 都由脸书维护。 [*Vite*](https://vitejs.dev/) (读作“veet”，由[尤雨溪](https://github.com/yyx990803)创建)是创建 React app 的替代选项。这是一个现代的 web 开发和快速的构建工具。它可以使用开发服务器提供代码，并为生产捆绑代码。支持 *Vue* 、React、 *Preact* 、 *lit* 、 *Svelte、*和 vanilla *JavaScript* 项目等框架。此外，它对*打字稿*、 *JSX* 、 *CSS* 以及更多的东西都有现成的支持。你可以在这里阅读 Vite [的其他功能。](https://vitejs.dev/guide/features.html)

视情况而定，你可能想也可能不想使用 Vite。例如，如果有人已经在使用 CRA，那么他们需要进行一次迁移，根据项目的大小，这可能容易也可能困难。另一方面，如果有人刚刚开始一个新项目，那么他们可以考虑使用 Vite。从这篇文章中，你可以学习使用 Vite 创建 React 应用程序的多种方法。

## 先决条件

我使用 macOS 进行设置。确保你已经安装了 [*node.js*](https://nodejs.org/en/) 和 [*yarn*](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable) 。我个人使用 [*nvm*](https://github.com/nvm-sh/nvm) (节点版本管理器)安装管理 node.js 的不同版本，我使用的 Node 和 yarn 版本是:

```
node --version
v18.4.0
yarn --version
1.22.19
```

现在，下面我有两个设置选项。两个选项产生相同的结果。看你个人喜好，两个都可以选。我更喜欢第二种选择，因为我可以少打字！

## 设置选项 1

首先，您需要运行以下命令:

```
yarn create vite
```

这里我把`react-vite`作为项目名称。

```
✔ Project name: … react-vite
```

选择`react`作为框架(使用上下键在选项间导航):

```
✔ Select a framework: › react
```

通过选择`react-ts`添加打字稿:

```
✔ Select a variant: › react-ts
```

最后，将目录更改为项目目录，安装所有依赖项，并启动本地开发服务器。

```
cd react-vite
yarn install
yarn run dev
```

现在，使用您最喜欢的 web 浏览器打开以下 URL:

```
http://localhost:5173/
```

您应该会看到以下网页:

![](img/0c7ab8b0f0f9fbab54a6a2148d820f3c.png)

React app — Image by Author

## 设置选项 2

这是一个非常简单的设置。键入以下命令，其中项目名称为`react-vite`:

```
yarn create vite react-vite --template react-ts
```

现在将目录更改为项目目录，安装所有依赖项，并启动本地开发服务器。

```
cd react-vite
yarn install
yarn run dev
```

官方文件可以在这里找到[。太棒了，现在你知道如何使用 Vite 创建一个 React 应用程序了！](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)

在这篇文章中，我们学习了什么是 Vite，以及如何使用 Vite 创建一个 React 应用程序。你可以从 [GitHub](https://github.com/lifeparticle/react-vite) 下载这个库。现在，您可以开始开发下一款 React 应用，节省开发时间。编码快乐！

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**