# 使用 TypeScript 创建快速样板文件

> 原文：<https://javascript.plainenglish.io/create-an-express-boilerplate-with-typescript-810eb6c29196?source=collection_archive---------2----------------------->

## 后端 API 入门的最低要求

![](img/be348ed520b4d053aaa9e0c6d1e8b9d1.png)

Photo by [Marvin Meyer](https://unsplash.com/@marvelous?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Express 是 Node.js 应用程序最流行的框架。它非常通用，没有任何限制。所以你可以随心所欲，随心所欲地设计你的应用程序。

今天，我们将使用 Express 来创建一个 HTTP 服务器，它可以接收请求，并看看如何用所需的中间件正确地设置它。

如果你想要一个没有明确支持的样板文件，你可以参考下面的文章。

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是这个系列的一部分。你可以在下面找到所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request Validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

我们开始吧！

## 获取 Node.js 样板文件

让我们首先克隆[样板存储库](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton)，在这里我们有一个工作 Node.js 应用程序，已经设置了 TypeScript、ESLint 和 Prettier。我们将在此基础上集成 Express。

```
git clone [https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton.git](https://github.com/Mohammad-Faisal/nodejs-typescript-skeleton.git)
```

## 安装依赖项

然后进入项目内部并安装依赖项:

```
cd nodejs-typescript-skeleton
yarn add Express
```

另外，添加 Express 模块的类型定义:

```
yarn add -D @types/express
```

## 测试一下！

进入 src/index.ts 文件，导入依赖项，并创建一个基本的 Express 应用程序:

```
import express, { Application, Request, Response } from "express";const app: Application = express();
```

然后，让我们创建一个接受 GET 请求并返回结果的基本路由:

```
app.get("/", async (req: Request, res: Response): Promise<Response> => {
  return res.status(200).send({
    message: "Hello World!",
  });
});
```

然后在端口 3000 上启动服务器:

```
const PORT = 3000;try {
  app.listen(PORT, (): void => {
    console.log(`Connected successfully on port ${PORT}`);
  });
} catch (error: any) {
  console.error(`Error occured: ${error.message}`);
}
```

然后运行应用程序:

```
yarn dev
```

继续点击下面的 URL `http://localhost:3000/`，你应该会看到下面的回应:

```
{ "message": "Hello World!" }
```

## 添加 Bodyparser

现在，这是开始使用 Express 的最低要求。但是在现实生活中，我们需要一些东西来让服务器正常工作。

为了在 Express 中处理 HTTP POST 请求，我们需要安装一个中间件模块 [body-parser](https://www.npmjs.com/package/body-parser) 。

让我们先安装它:

```
yarn add body-parser
yarn add -D @types/body-parser
```

然后在 index.ts 文件中使用它:

```
import bodyParser from "body-parser";const app: Application = express();app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
```

并添加另一个路由来处理 HTTP POST 请求:

```
app.post("/post", async (req: Request, res: Response): Promise<Response> => {
  console.log(req.body);
  return res.status(200).send({
    message: "Hello World from post!",
  });
});
```

您会注意到，在路由处理程序中，我们可以通过以下方式获取请求体:

```
req.body;
```

这是可能的，因为使用了 body-parser。

## 结论

就是这样。现在，您已经有了一个可以接收 HTTP 请求的基本 express 应用程序。

希望你今天学到了新东西。祝您愉快！

***想连接？***

*可以通过*[***LinkedIn***](https://www.linkedin.com/in/56faisal/)*或者我的* [***个人网站***](https://www.mohammadfaisal.dev/blog) ***联系我。***

# Github 知识库

[](https://github.com/Mohammad-Faisal/express-typescript-skeleton) [## GitHub-Mohammad-fais al/express-Typescript-skeleton:支持类型脚本的 ExpressJS 样板文件

### 今天我们将把 Typescript 与 NodeJS 样板文件集成在一起。如果您对如何使用…设置 Typescript 感兴趣

github.com](https://github.com/Mohammad-Faisal/express-typescript-skeleton) 

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**