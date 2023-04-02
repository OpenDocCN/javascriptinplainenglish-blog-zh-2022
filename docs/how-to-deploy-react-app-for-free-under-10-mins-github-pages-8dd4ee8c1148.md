# 如何在 10 分钟内免费部署 React 应用程序- GitHub 页面

> 原文：<https://javascript.plainenglish.io/how-to-deploy-react-app-for-free-under-10-mins-github-pages-8dd4ee8c1148?source=collection_archive---------2----------------------->

![](img/091415378ce30f3ed27963e389170b49.png)

现在 Heroku 已经结束了它的免费层计划，GitHub Pages 是部署基于 React 的 web 应用程序的最佳解决方案之一。在本文中，我将指导您如何在 10 分钟内部署 React 应用程序。

**先决条件:**

*   GitHub 上托管的 React 应用
*   GitHub Pro 帐户托管私有代码(稍后将详细介绍)

我假设您已经安装并运行了 React 应用程序，并且托管在 GitHub 存储库中。

我们开始吧

1.  **安装** `**gh-pages**` **npm 包**

我们将使用 gh-pages 包来快速部署我们的应用程序，通过在终端上运行以下命令来安装`gh-pages`作为开发依赖项。

```
$ npm install gh-pages --save-dev
```

**2。将首页属性添加到** `**package.json**` **文件**

我们需要在`package.json`中设置`homepage`属性，这必须是您的站点将被托管的 URL，根据您的项目，它可以是用户站点或项目站点，两者的格式如下-

*   *用户站点* : `https://{username}.github.io`
*   *项目地点* : `https://{username}.github.io/{repo-name}`

比如我的用户名是 [prathamesh-mutkure](https://github.com/prathamesh-mutkure) ，那么我的主页属性应该是`[https://prathamesh-mutkure.github.io](https://prathamesh-mutkure.github.io)`

你的`package.json`现在应该看起来像这样

```
{
"homepage": "https://prathamesh-mutkure.github.io",
"name": "personal-site",
"version": "0.1.0",
"private": true,
...
}
```

**3。将部署脚本添加到** `**package.json**` **文件**

现在将`predeploy`和`deploy`脚本添加到`package.json`文件中的`scripts`属性中，现在看起来应该是这样的

```
"scripts": {
+   "predeploy": "npm run build",
+   "deploy": "gh-pages -d build",
    "start": "react-scripts start",
    "build": "react-scripts build",
    ...
}
```

**4。部署 React 应用程序**

最后，运行以下命令来部署您的应用程序-

```
$ npm run deploy
```

恭喜，您的 react 应用程序现已在🥳上线

# 自定义域

在 GitHub 页面上设置一个自定义域非常简单，只需进入你的库然后`setting`，然后在`pages`下，你将能够在页面底部添加一个自定义域。

如果您已经为您的用户站点设置了一个自定义域，那么您可以跳过这一步，GitHub 会自动将项目站点路由到您的自定义域。:)

# 托管私有代码

GitHub pages 的一个缺点是，它只允许你托管公共存储库，要托管私人回购的代码，你需要 GitHub Pro 帐户。

但是如果你是一名学生，我有一些好消息要告诉你——你可以在 GitHub 教育包下免费获得 GitHub Pro 的所有好处，它还为学生提供了许多额外的好处。

我将很快为印度学生制作另一个博客，介绍如何以高成功率申请教育包，请务必关注我，以免浪费几周的时间。

*快乐黑客，Prathamesh :)*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*