# 免费在 Github 页面上放一个 React 应用

> 原文：<https://javascript.plainenglish.io/put-a-react-app-on-github-pages-570d0e90a30d?source=collection_archive---------2----------------------->

## 向你的朋友免费展示你的精美动态页面，给潜在雇主留下深刻印象。

![](img/d81c68881e5f5fef8665776ad82bb398.png)

Photo by [Roman Synkevych](https://unsplash.com/@synkevych?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Github Pages 是免费发布自己网站的好方法。每个用户获得一个带有 URL 的页面。例如，用户“fzappa”可以使用`https://fzappa.github.io`。缺点是，如果你按照 Github Pages [网站](https://pages.github.com/)上的说明去做，你只是在构建一个静态网页。好消息是你不必满足于此。有一种方法可以使用 React 应用程序，这样你就可以向你的朋友展示你精美的动态页面，给潜在的雇主留下深刻印象。

首先要做的是为你的站点创建一个 Github 存储库。有一个命名惯例要遵循，否则它不会工作。确保您的新公共回购的名称是`username.github.io`，其中“用户名”是您的用户名。

接下来，创建您的 React 应用程序。在你的终端:`npx create-react-app my-page`

用`my-page`代替您选择的应用程序名称。需要注意的一点是，create-react-app 不再支持全局安装，所以你可能需要先运行`npm install create-react-app`。一旦 create-react-app 完成了它的工作，进入新应用程序的目录:

```
cd my-page
```

在新 app 安装目录下`gh-pages`:

```
npm install gh-pages --save-dev
```

接下来，进入`package.json`并添加以下属性，其值为您的 Github 页面 URL:

```
"homepage": "https://username.github.io"
```

确保使用您的个人用户名代替“用户名”,并且`package.json`文件的顶部应该看起来像这样:

导航到`package.json`中的`"scripts"`对象，添加两个名为`predeploy`和`deploy`的属性，其值如下:

接下来在终端中输入`npm run deploy`,它会将应用程序部署到您的 Github Pages 地址。运行这个将在 Github 存储库中创建一个`gh-pages`分支。在 Github 页面上正确运行 React 应用程序需要这个分支中的代码。要确保这一点，请在 Github Pages repo 中进入“设置”并导航至“页面”。在“Source”部分，确保`gh-pages`分支是构建 Github Pages 站点的分支。

现在，当你访问 Github 页面的 URL 时，你的 React 应用程序应该在那里。Github 库中唯一的东西是`gh-pages`分支。要添加应用程序的源代码，您需要添加远程存储库:

```
git remote add origin [https://github.com/username/username.github.io.git](https://github.com/username/username.github.io.git)
```

然后推送源代码，确保推送至主分支:

```
git push origin main
```

您的 Github 存储库现在将有一个包含应用程序源代码的`main`分支。对应用程序所做的任何更改都可以推送到这个分支。确保在对 React 应用程序进行修改后再次运行`npm run deploy`。如果你不想使用标准的 Github pages 域名，有一种方法可以创建一个自定义域名，方法是在应用程序的`public`文件夹中添加一个名为`CNAME`的文件。然后把你的自定义名字放进去:`mycustomname.com`

确保更改`package.json`中`"homepage"`的值，以匹配新的自定义域。

现在，您可以炫耀那个花哨的动态投资组合网站或项目，而不必满足于静态页面。最棒的是，这一切都是免费的。每个 Github 用户都有一个页面，所以最好充分利用它！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***