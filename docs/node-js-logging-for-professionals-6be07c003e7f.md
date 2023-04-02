# 专业人员的 Node.js 日志记录

> 原文：<https://javascript.plainenglish.io/node-js-logging-for-professionals-6be07c003e7f?source=collection_archive---------0----------------------->

## 发挥温斯顿和摩根的全部潜力

![](img/f62f31e03f1632eb4c1d1340546702cc.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

日志记录是任何生产级应用程序的重要组成部分。这是最重要的部分之一。

今天我们将学习如何在 Node.js 中有效地使用日志记录，以及如何在生产级应用程序中使用日志记录。

## 在我们开始之前…

我用 ExpressJS 和 Typescript 创建了一个[专业样板。本文是这个系列的一部分。你可以在下面找到所有的文章。](https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate)

```
***** [**Creating a ExpressJS + Typescript Boilerplate**](/create-an-express-boilerplate-with-typescript-810eb6c29196) ***** [**How to setup Linter and Formatter for NodeJS**](/how-to-set-up-linter-formatter-for-node-js-d6b34c0c8be5) ***** [**How to handle multiple environments in NodeJS**](https://blog.devgenius.io/how-to-handle-multiple-environments-in-nodejs-7391d2db2abe) ***** [**Error Handling in NodeJS**](/error-handling-in-node-js-like-a-pro-ed210baa0600) ***** [**Request validation in NodeJS**](https://medium.com/p/c69f2494cf18) ***** [**Using Docker Professionally with NodeJS**](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) ***** [**Using Docker for Local Development in NodeJS**](/node-js-database-with-docker-for-local-development-285212c5162f) ***** [**Logging in NodeJS**](/node-js-logging-for-professionals-6be07c003e7f) ***** [**Kubernetes with NodeJS**](https://levelup.gitconnected.com/kubernetes-deployment-with-nodejs-made-easy-eaeec32b62e3)
```

我们开始吧！

# 选择

Node.js 有很多很好的日志库，其中最流行的当然是 [winston](https://www.npmjs.com/package/winston) 。这是一个通用日志库，能够满足您所有的日志需求。

此外，还有一个专门用于 HTTP 请求的库。那个叫[的摩根](https://www.npmjs.com/package/morgan)。

今天，我们将在应用程序中使用这两个库。

# 出发点

今天，我们将在用 TypeScript 构建的现有 Node.js 应用程序上集成日志记录。您可以在下面的文章中了解更多关于我们如何构建它的信息:

[](https://www.mohammadfaisal.dev/blog/create-express-typescript-boilerplate) [## 创建-快递-打字稿-样板文章|穆罕默德·费萨尔

### ExpressJS 是 NodeJS 应用程序最流行的框架。它非常通用，没有任何限制。所以你…

www.mohammadfaisal.dev](https://www.mohammadfaisal.dev/blog/create-express-typescript-boilerplate) 

但是你可以自由使用任何你喜欢的应用程序。

# 拿样板文件

让我们首先克隆[样板存储库](https://github.com/Mohammad-Faisal/express-typescript-skeleton)，在这里我们有一个工作 Node.js 应用程序，已经设置了 TypeScript、ESLint 和 Prettier。

```
git clone [https://github.com/Mohammad-Faisal/express-typescript-skeleton.git](https://github.com/Mohammad-Faisal/express-typescript-skeleton.git)
```

# 安装依赖项

然后进入项目内部并安装依赖项。

```
yarn add winston
```

然后创建一个记录器实例。

logger.ts

在这个配置中，`createLogger`函数是从 Winston 库中导出的。我们已经通过了两个选项。

`**format**` - >表示我们想要的格式。我们已经指定，我们希望我们的日志是 JSON 格式，并包括时间戳。

`**transports**` - >表示我们的日志要放在哪里。我们定义我们希望我们的错误日志到一个名为`errors.log`的文件中。

现在让我们在`index.ts`文件中创建它。

```
import logger from "./logger";logger.error("Something went wrong");
```

如果我们运行这段代码，我们会看到一个名为`errors.log`的新文件被创建，并且会有一个条目。

```
{ 
  "level": "error", 
  "message": "Something went wrong", 
  "timestamp": "2022-04-16T12:16:13.903Z" 
}
```

这是登录我们的应用程序的最基本的格式。

# 将开发日志放入控制台。

在开发我们的应用程序时，我们不希望每当出现错误时就检查我们的错误日志文件。我们希望它们直接进入控制台。

我们已经讨论过传输，它们是我们给出日志输出的通道。让我们为控制台创建一个新的传输，并在开发模式中添加它。

logger.ts

此配置会将所有日志发送到控制台。

如果您仔细观察，您会发现我们正在向我们的日志添加一些格式:

```
format: format.combine(format.colorize(), format.simple()),
```

我们将开发日志着色，并保持简单。你可以在这里看看可能的选择:

[](https://github.com/winstonjs/logform#readme) [## GitHub - winstonjs/logform:一种可变的对象格式，设计用于链接& objectMode 流

### 一种可变的基于对象的日志格式，设计用于链接& objectMode 流。提供给给定的信息参数…

github.com](https://github.com/winstonjs/logform#readme) 

# 服务特定日志

有时我们希望更好地分隔日志，并希望对日志进行分组。我们可以通过在选项中指定一个服务字段来做到这一点。假设我们有一个计费服务和认证服务。我们可以为每个实例创建一个单独的记录器。

```
const logger = createLogger({
  defaultMeta: {
    service: "billing-service",
  },
  //... other configs
});
```

这一次，我们所有的日志都将采用类似这样的格式。

```
{
  "level": "error",
  "message": "Something went wrong",
  "service": "billing-service",
  "timestamp": "2022-04-16T15:22:16.944Z"
}
```

这有助于分析日志信件。

# 我们可以做得更好。

有时我们需要单独的日志级控制。例如，如果我们想要跟踪用户的流量，我们可能需要为每一级信息添加信息。这对于服务级别定制是不可能的。

为此，我们可以使用`[child-logger](https://github.com/winstonjs/winston#creating-child-loggers)`

这个概念允许我们注入关于单个日志条目的上下文信息。

```
import logger from "./utils/logger";const childLogger = logger.child({ requestId: "451" });childLogger.error("Something went wrong");
```

这一次，我们将为每个请求 id 获取单独的错误日志，以便稍后进行过滤。

```
{
  "level": "error",
  "message": "Something went wrong",
  "requestId": "451",
  "service": "billing-service",
  "timestamp": "2022-04-16T15:25:50.446Z"
}
```

我们还可以记录异常和未处理的承诺拒绝，以防失败。`**winston**`为我们提供了一个很好的工具。

winston.ts

# 衡量绩效。

我们可以通过使用这个记录器来分析我们的请求:

logger.ts

这将给出关于性能的附加输出。

```
{ 
  "durationMs": 5, 
  "level": "info", 
  "message": "meaningful-name", 
  "timestamp": "2022-03-12T17:40:59.093Z" 
}
```

你可以在这里看到更多关于`winston`的例子:

[](https://github.com/winstonjs/winston/tree/master/examples) [## winstonjs 大师的例子

### 几乎所有事情的记录者。在 GitHub 上创建一个帐户，为 winstonjs/winston 开发做贡献。

github.com](https://github.com/winstonjs/winston/tree/master/examples) 

# 利用摩根

至此，您应该明白为什么 Winston 即使不是最好的，也是最好的日志库之一。但是它是用于通用日志记录的。

另一个库可以帮助我们进行更复杂的日志记录，特别是对于 HTTP 请求。那个图书馆叫做[摩根](https://www.npmjs.com/package/morgan)。

首先，创建一个将拦截所有请求的中间件。我正在将它添加到`middlewares/morgan.ts`文件中:

morganMiddleware.ts

注意我们是如何修改流方法来使用 Winston 记录器的。morgan 有一些预定义的日志格式，如 tiny 和 combined，您可以使用如下格式:

```
const morganMiddleware = morgan("combined", {
  stream,
  skip,
});
```

这将以单独的格式输出。

现在在`index.ts`文件中使用这个中间件:

```
import morganMiddleware from "./middlewares/morgan";app.use(morganMiddleware);
```

现在，所有的 out 请求都将记录在 Winston 的 HTTP 层中。

```
{ "level": "http", "message": "GET /ping 304 - - 11.140 ms ::1\n", "timestamp": "2022-03-12T19:57:43.166Z" }
```

这样，您也可以维护所有 HTTP 请求引用。

# 根据类型分离日志

所有的日志都不一样。您可能需要将错误日志和信息日志分开。我们之前讨论了传输以及它如何帮助我们将日志流式传输到不同的目的地。

我们可以利用这个概念，过滤日志，并把它们发送到不同的目的地。

让我们为我们的日志创建一些过滤器！

filter.ts

然后修改我们的传输阵列以利用这一点:

logger.ts

如果仔细观察，您会发现每种类型的日志都有三个单独的日志文件。

# 日志文件的每日循环

现在，在生产系统中，维护这些日志文件可能会很痛苦。因为如果您的日志文件太大，那么一开始就没有必要保存日志。

我们必须轮换我们的日志文件，还需要有一种方法来组织它们。

这就是为什么有一个叫做[的漂亮模块。](https://www.npmjs.com/package/winston-daily-rotate-file)

我们可以用它来进行配置，这样我们的日志文件每天都会轮换，我们还可以传入大量的配置，比如文件的最大大小。

首先，安装它:

```
yarn add winston-daily-rotate-file
```

然后在`winston`内更换我们的运输机:

```
const infoTransport: DailyRotateFile = new DailyRotateFile({
  filename: "logs/info-%DATE%.log",
  datePattern: "HH-DD-MM-YYYY",
  zippedArchive: true,
  maxSize: "20m",
  maxFiles: "14d",
  level: "info",
  format: format.combine(infoFilter(), format.timestamp(), json()),
});
```

对所有日志级别都这样做，并在 Winston 中的传输中传递它:

```
transports: [new transports.Console(), httpTransport, infoTransport, errorTransport],
```

现在，您将在以指定格式命名的日志文件夹中看到新的日志文件。

这应该可以解决你所有的日志问题。

# 最终版

我们已经介绍了登录 Node.js 应用程序的一些主要概念。让我们把它们派上用场。

我们可以将所有的逻辑封装到一个单独的类中，如下所示:

我们可以像下面这样使用它:

```
import { Logger } from "./utils/Logger";// middleware for morgan
app.use(Logger.getHttpLoggerInstance());const logger = Logger.getInstance();
```

希望你今天学到了新东西！

点击这里，你可以获得这篇文章的所有[代码片段](https://code.pieces.app/partner-collections/how-to-add-production-grade-nodejs-logging)

***想要连接？***

*可以通过*[***LinkedIn***](https://www.linkedin.com/in/56faisal/)*或者我的* [***个人网站***](https://www.mohammadfaisal.dev/blog) ***联系我。***

# Github 资源库:

[](https://github.com/Mohammad-Faisal/nodejs-logging-for-production) [## GitHub-Mohammad-fais al/nodejs-生产日志:如何设置生产级日志…

### 日志记录是任何生产级应用程序的重要组成部分。事实上，这是最重要的部分之一。今天…

github.com](https://github.com/Mohammad-Faisal/nodejs-logging-for-production) [](/error-handling-in-node-js-like-a-pro-ed210baa0600) [## 像专家一样处理 Node.js 中的错误

### 你需要知道的一切。

javascript.plainenglish.io](/error-handling-in-node-js-like-a-pro-ed210baa0600) [](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [## 像专业人士一样使用 Docker 和 NodeJS 项目！

### 在开发和生产中利用 Docker 的力量

levelup.gitconnected.com](https://levelup.gitconnected.com/use-docker-with-nodejs-projects-like-a-pro-a9e7504e1308) [](/node-js-database-with-docker-for-local-development-285212c5162f) [## Node.js +带有 Docker 的数据库，用于本地开发

### 各种数据库的一站式解决方案。

javascript.plainenglish.io](/node-js-database-with-docker-for-local-development-285212c5162f) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/) *与* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***