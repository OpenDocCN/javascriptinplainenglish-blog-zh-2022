# TypeScript 中 Express & React 全栈应用程序的配方

> 原文：<https://javascript.plainenglish.io/recipes-for-express-and-react-fullstack-apps-in-type-8bcd4644bed0?source=collection_archive---------8----------------------->

## 如何使用 TypeScript 在 Express 中构建优雅的全栈应用

![](img/2d9f978b1d215b98fd68919b9a38df3c.png)

Photo by [Chris Liverani](https://unsplash.com/@chrisliverani?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/fast?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我用 Flask 用 Python 写了不少应用后端，所以想试试它的 JavaScript 表亲 Express。

我找到了一些关于如何在全栈应用中做到这一点的教程。然而，它们似乎都不太详细。我感兴趣的是如何编写一些可以很好地扩展以包括许多路由，容易与前端集成，以及如何将其全部容器化的东西。

这就是这篇文章的内容😏如果你想直接跳到代码，点击[这里](https://github.com/osintalex/express-react-poc)。(没有判断，我在看文章的时候一直都是这样😉).

## 概观

首先，这里是我想通过这个概念验证解决的所有问题:

1.  拥有超级模块化的应用配置方式，即轻松允许不同的开发、生产和测试值；
2.  采用模块化方式处理申请路线；
3.  有一种处理数据库操作的方法，愉快地注入数据库依赖关系，最好这样它们可以在测试中很容易地模拟出来；
4.  将 React 应用程序与 express 应用程序捆绑在一起的非常简单的方法；
5.  一个容器化应用的最终交付物；
6.  具有预提交挂钩的良好代码林挺；
7.  所有东西都是打字稿！

首先，这是我的应用程序布局的样子:

```
backend/
--package.json
--tsconfig.json
--yarn.lock
--src/
  --index.ts //entrypoint
  --configs/
  --controllers/
  --db/
  --models/
  --tests/frontend/
  --package.json
  --tsconfig.json
  --yarn.lock
  --src/
    --index.tsx //entrypoint
    --App.tsx
```

正如你从上面看到的，我在反应部分没有做任何工作。我刚刚确保您可以轻松集成 React 应用程序，这意味着您的应用程序有一个很好的前端，您可以对后端进行 API 调用，而不会出现任何问题。

## 模块化配置

我真的很喜欢在 Python 中这样做的典型方式，因为它使得在不同配置之间切换变得如此容易。下面是在一个`backend/src/configs/config.ts`文件中的 TypeScript 中的样子。

我认为这很酷的原因是，你可以在应用程序的任何地方做这样的事情:

```
import { configByEnvironment, environmentName, ConfigType } from "./configs/config";const configuration: *ConfigType* = configByEnvironment(environmentName);
const { port } = configuration;app.use(morgan(configuration.morganFormat));
```

所以你只需要修改`config.ts`文件中的内容就可以了——很简单。

## 模块化路线

这非常简单，但我花了一段时间才从网上阅读的材料中弄明白，所以下面是我如何做的，以防其他人发现它有用:

在`controllers/`内这样定义路线:

然后你可以像这样在`index.ts`中注册它们:

```
import example from "./controllers/example";
import express, { Express} from "express";const app: *Express* = express();
app.use("/example", example);
```

## 数据库依赖性

我发现最简洁的方法是使用`typeorm`并在我的`db`目录中定义一个这样的数据库读取操作模块:

第 28 行非常关键——这使得在测试中模拟数据库操作变得非常容易，并且很容易将读取报告放到视图中。回头看看上面控制器中的`example.ts`文件，明白我的意思。

为了测试，我发现很容易用 sinon 来模拟这一点:

..这样你就不必做任何奇怪的事情，从`typeorm`库或者你正在使用的任何其他 ORM 中模仿更大范围的方法。

## 与 React 捆绑

这在你的`index.ts`里很容易做到。你所要做的就是:

```
app.get("*", (*_req*: *Request*, *res*: *Response*): *void* => {*res*.sendFile(configuration.frontendStaticFilesPath, "index.html");});
```

其中`frontendStaticFilesPath`指向运行`react-scripts build`产生的构建输出。我认为这非常好，因为它避免了您在全栈工作时经常遇到的一些其他问题:

*   无需进行任何 CORS 配置😍。你的前端实际上和你的后端在同一个原点上！
*   您可以非常轻松地在一个容器中运行所有内容，无需分离前端或后端服务。当然，你可能会因为其他原因想这么做，比如缩放等等，但是对于一个快速原型，我认为这是🆒

这使我想到…

## 将您的应用容器化

由于一切都在一个服务中运行，并且因为您的 TypeScript 正在编译为 JavaScript，所以您可以通过如下三阶段构建将一切巧妙地结合在一起:

这将产生一个超级轻量级的最终映像，它作为非根用户节点运行，并利用了`pm2`。如果你对我在这里做出的一些选择感到好奇，在 Docker [这里](/build-a-production-ready-node-express-api-with-docker-9a45443427a0)有一篇关于发布快递应用的很好的文章。

## 代码林挺

有很多方法可以设置 ESLint，所以我就不深究了。我建议阅读一些关于如何做到这一点的具体帖子，或者如果你不介意，那么就使用`npx eslint init`或它的等效物`yarn eslint init`。

一旦这样做了，尽管将 husky 添加到全栈应用程序设置中有点麻烦，例如，带有 2 个`package.json`文件的 repo。

我是这样做的:

```
// Add this to package.json scripts in backend
"prepare": "cd .. && husky install backend/.husky"
// Add this in frontend
"prepare": "cd .. && husky install frontend/.husky"
```

然后在前端目录中，你可以点击`yarn prepare`然后`yarn husky add .husky/pre-commit "cd frontend && <lint command goes here>"`，然后对后端做完全相同的事情。

这就对了。希望这有帮助。😅

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*