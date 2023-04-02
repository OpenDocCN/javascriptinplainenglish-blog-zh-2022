# 了解 Winston js—node . js 中的主日志记录

> 原文：<https://javascript.plainenglish.io/learn-winstonjs-master-logging-in-node-js-d00f43df6496?source=collection_archive---------6----------------------->

## winstonjs 入门所需的一切。

![](img/217672c059527ed49d6bde52a2375eaa.png)

Photo by [Mildly Useful](https://unsplash.com/@usefulcollective?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Winston 是一个易于使用且灵活的日志库。在本教程中，我们将涵盖你需要开始的一切。

# **入门**

在本教程中，我将建立一个简单的应用程序，但是您可以自由地跟随您自己的项目。如果您正在使用自己的项目，可以跳到下一部分。

1.  为您的项目创建新目录。
2.  运行`npm init -y`(或`yarn init`)创建一个空白的 NPM 项目。
3.  用`npm i winston`(或`yarn add winston`)安装温斯顿。
4.  创建一个名为`index.js`的新文件，并添加以下样板代码。
5.  用`node .`运行应用程序，确认 web 服务器已经启动(在本教程的剩余部分，我们将使用这个命令来启动应用程序)
6.  在 [http://localhost:8080](http://localhost:8080) 访问任何路由，以显示它正在工作
7.  通过访问[http://localhost:8080/stop](http://localhost:8080/stop)停止服务器

```
const { createServer } = require('http')/**
 * My test app
 */
class App {
  constructor() {
    this.server = createServer((req, res) => {
      // if someone visits [http://localhost:8080/stop](http://localhost:8080/stop)
      // then stop the server
      if (req.url === '/stop') {
        res.writeHead(200, { 'Content-Type': 'application/json' })
        res.end(JSON.stringify({
          message: 'Server is stopping'
        }))
        return this.stop()
      }// otherwise, just send a simple response
      res.writeHead(200, { 'Content-Type': 'application/json' })
      res.end(JSON.stringify({
        message: 'Hello World'
      }))
    })
  }/**
   * Start the server
   */
  start() {
    this.server.listen(8080)
  }/**
   * Stop the server
   */
  stop() {
    this.server.close()
    process.exit(0)
  }
}let app = new App()
app.start()
```

# **创建我们的记录器**

现在我们有一个项目要做，让我们用推荐的配置创建一个 Winston 记录器的实例。如果你有多个文件，我建议把它放在你的应用程序的类中，但是为了简单起见，我会把它作为一个全局对象放在我的文件的顶部(在导入之后)。

```
const winston = require('winston')
// ESModules
import winston from 'winston'const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: { service: 'user-service' },
  transports: [
    //
    // - Write all logs with importance level of `error` or less to `error.log`
    // - Write all logs with importance level of `info` or less to `combined.log`
    //
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' }),
  ],
})
```

我们可以看到，在这个默认配置中，我们将日志输出到两个不同的文件中。错误进入`error.log`，所有日志进入`combined.log`。我们还使用 JSON 格式作为输出。这样我们就可以更清楚地看到这会产生什么，给“开始”和“停止”函数添加一些日志，或者如果你正在使用你自己的项目，找到你自己的开始和停止代码并添加一些日志来显示发生了什么。

```
 start() {
    logger.info('Starting the server')
    ...
  } stop() {
    logger.info('Stopping the server')
    ...
  }
```

在此之后运行应用程序会创建 2 个日志文件。然而，我们在终端中看不到任何东西。默认情况下，Winston 不会在任何地方记录日志，所以我们必须使用传输明确地告诉它将日志发送到哪里。我们已经使用文件传输将它们发送到我们的文件中，并且我们可以添加一个控制台传输来记录到控制台。

Winston 提供了一点不错的样板文件，只在开发过程中记录到控制台。在创建记录器的位置下添加以下代码。

```
if (process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.simple(),
  }));
}
```

如你所见，我们还可以选择其他格式。“简单”格式将您的日志显示到控制台，如下所示。

```
info: Starting the server {“service”:”user-service”}
```

向您的项目添加一些日志(比如记录传入的请求)，然后继续下一步，我们将创建自己的传输。

# **定制运输**

自定义传输很容易创建，可以做各种各样的事情。下面的例子把我们的日志作为一个 webhook 发送到另一个服务器(这对于集中日志记录很有用)。在构造函数中，我们要求一个 url 参数，如果我们没有得到，就抛出一个错误。然后，我们可以在 log 方法中使用它将我们的 webhook 发送到 url。

```
class CustomTransport extends winston.Transport {
  constructor(opts) {
    super(opts);
    if (!opts.url) throw Error('URL not provided')
    this.url = opts.url
  }log(info, callback) {
    setImmediate(() => {
      this.emit('logged', info);
    });// Send a webhook, write to a file, or anything else you wish to do with the log
    fetch(this.url, {
      method: 'post',
      body: {
        info
      }
    })
    callback();
  }
}
```

我们可以将我们的传输添加到我们的日志配置中，并指定我们需要的任何选项。

```
const winston = require('winston')
// ESModules
import winston from 'winston'const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: { service: 'user-service' },
  transports: [
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' }),
    // remember to pass in any options you defined
    new CustomTransport({ url: '[https://example.com/logging'](https://example.com/logging') }),
  ],
})
```

# **结论**

像 Winston 这样的库的优点是为任何用例提供了一个简单、灵活、可定制的记录器。无论是通过自定义传输向开发人员发送电子邮件来报告错误，还是简单地登录到开发中的控制台。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***