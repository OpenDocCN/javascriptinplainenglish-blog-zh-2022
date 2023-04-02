# 像专家一样处理 Node.js 中的错误

> 原文：<https://javascript.plainenglish.io/error-handling-in-node-js-like-a-pro-ed210baa0600?source=collection_archive---------2----------------------->

## 你需要知道的一切。

![](img/574b68e0ee885c8fb01f06829369ca7c.png)

Photo by [ThisisEngineering RAEng](https://unsplash.com/@thisisengineering?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology-error?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

处理错误是任何生产级应用程序最重要的方面之一。任何人都可以为成功案例编写代码。只有真正的专业人士会处理错误案例。

今天我们将学到这一点。让我们开始吧。

首先，我们必须明白，并非所有的错误都是一样的。让我们看看在一个应用程序中会出现多少种错误。

*   用户产生的错误
*   硬件故障
*   运行时错误
*   数据库错误

我们将看到如何轻松处理这些不同类型的错误。

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是这个系列的一部分。你可以在下面找到所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request Validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

我们开始吧！

# 获取基本的快速应用程序。

运行以下命令以获得用 typescript 构建的基本 express 应用程序。

```
git clone [https://github.com/Mohammad-Faisal/express-typescript-skeleton.git](https://github.com/Mohammad-Faisal/express-typescript-skeleton.git)
```

# 处理找不到 URL 错误

如何检测在您的 express 应用程序中点击的 URL 是否处于非活动状态？你有一个类似于`/users,`的 URL，但是有人点击了`/user.`，我们需要通知他们，他们试图访问的 URL 不存在。

这在 ExpressJS 中很容易做到。定义所有路由后，添加以下代码来捕获所有不匹配的路由，并发送回正确的错误响应。

main.ts

这里我们使用`“*”`作为通配符来捕捉所有没有通过我们的应用程序的路由。

# 用特殊的中间件处理所有错误

现在我们在 Express 中有一个特殊的中间件来处理我们所有的错误。我们必须将它包含在所有路由的末尾，并从顶层向下传递所有错误，以便这个中间件可以为我们处理它们。

最重要的事情是把这个中间件放在所有其他中间件和路由定义之后，因为否则，一些错误会溜走。

让我们将它添加到索引文件中。

errormiddleware.ts

看看中间件签名。与其他中间件不同，这个特殊的中间件有一个名为`err`的额外参数，它属于`Error`类型。这是第一个参数。

并修改我们之前的代码，如下所示传递错误。

```
app.use("*", (req: Request, res: Response, next: NextFunction) => {
  const err = Error(`Requested path ${req.path} not found`);
  next(err);
});
```

现在，如果我们点击一个随机的 URL，比如，`http://localhost:3001/posta`，那么我们将得到一个正确的错误响应。

```
{
  "success": false,
  "message": "Requested path ${req.path} not found",
   "stack": "Error: Requested path / not found\n    at  
             /Users/mohammadfaisal/Documents/learning/express-  
             typescript-skeleton/src/index.ts:23:15\n"
}
```

# 自定义错误对象

让我们仔细看看 Node.js 提供的默认错误对象。

```
interface Error {
  name: string;
  message: string;
  stack?: string;
}
```

所以当你抛出如下错误时。

```
throw new Error("Some message");
```

那么你只能得到名字和可选的`stack`属性。这个堆栈为我们提供了错误产生的确切位置的信息。我们不想将它包含在生产中。我们稍后将看到如何做到这一点。

我们可能希望向错误对象本身添加更多的信息。

此外，我们可能希望区分不同的错误对象。

让我们为我们的应用程序设计一个基本的自定义错误类。

ApiError.ts

请注意下面一行。

```
Error.captureStackTrace(this, this.constructor);
```

它有助于从应用程序的任何地方捕获错误的堆栈跟踪。

在这个简单的类中，我们也可以添加`statusCode`。让我们像下面这样修改我们以前的代码。

err.ts

并利用错误处理程序中间件中新的`statusCode`属性

err.ts

自定义的错误类使您的 API 对最终用户来说是可预测的。大多数新手都错过了这一部分。

# 让我们来处理应用程序错误。

现在让我们也从我们的路由内部抛出一个自定义错误。

=ManualError.ts

这是人为制造的情况，我们需要抛出一个错误。在现实生活中，我们可能有很多情况需要使用这种 try/catch 块来捕捉错误。

如果我们点击下面的 URL，`http://localhost:3001/protected`，我们将得到下面的响应。

```
{
  "success": false,
  "message": "You are not authorized to access this!",
  "stack": "Some details"
}
```

所以我们的错误响应工作正常！

# 让我们改进这一点！

所以我们现在可以在应用程序的任何地方处理我们的自定义错误。但是它到处都需要一个 try-catch 块，并且需要用 error 对象调用`next`函数。

这并不理想。它会立刻让我们的代码看起来很糟糕。

让我们创建一个定制的包装函数，它将捕获所有的错误，并从一个中心位置调用下一个函数。

让我们为此创建一个包装器实用程序！

asyncWrapper.ts

并在我们的路由器中使用它。

wrapper.ts

运行代码，看看我们有相同的结果。这有助于我们消除所有的 try/catch 块，并到处调用下一个函数！

# 自定义错误的示例

我们可以根据需要微调我们的错误。让我们为未找到的路径创建一个新的错误类。

NotFoundError.ts

并简化我们的坏路由处理器。

```
app.use((req: Request, res: Response, next: NextFunction) => next(new NotFoundError(req.path)));
```

有多干净？

现在让我们安装一个小的软件包来避免我们自己编写状态代码。

```
yarn add http-status-codes
```

并以有意义的方式添加状态代码。

NotFoundError.ts

像这样在我们的路线里。

Error.ts

这让我们的代码变得更好。

# 处理程序员错误。

处理程序员错误的最好方法是优雅地重启。将下面一行代码放在应用程序的末尾。如果在错误中间件中没有捕捉到什么，它将被调用。

uncaughtException.ts

# 处理未处理的承诺拒绝。

我们可以记录拒绝承诺的原因。这些错误永远不会到达我们的快速错误处理程序。例如，如果我们想用错误的密码访问数据库。

unhandledRejection.ts

# 进一步改进

让我们创建一个新的 ErrorHandler 类来集中处理错误。

ErrorHandler.ts

这只是一个简单的错误处理器中间件。您可以在此添加您的自定义逻辑。并在我们的索引文件中使用它。

```
app.use(ErrorHandler.handle());
```

这就是我们如何通过尊重 SOLID 的单一责任原则来分离关注点。

你可以在这里 **找到这篇文章的所有 [**代码。**](https://github.com/Mohammad-Faisal/nodejs-expressjs-error-handling)**

我希望你今天学到了新东西。祝你今天休息愉快！

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

# 其他节点文章

[](/node-js-logging-for-professionals-6be07c003e7f) [## 专业人员的 Node.js 日志记录

### 发挥温斯顿和摩根的全部潜力

javascript.plainenglish.io](/node-js-logging-for-professionals-6be07c003e7f) [](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) [## 如何在 NodeJS 中处理多种环境

### 如何建立一个专业的节点工程

blog.devgenius.io](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) [](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [## 像专业人士一样使用 Docker 和 NodeJS 项目！

### 在开发和生产中利用 Docker 的力量

levelup.gitconnected.com](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [](/node-js-database-with-docker-for-local-development-285212c5162f) [## Node.js +带有 Docker 的数据库，用于本地开发

### 各种数据库的一站式解决方案。

javascript.plainenglish.io](/node-js-database-with-docker-for-local-development-285212c5162f) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*