# NestJS #1:创建您的第一个 API

> 原文：<https://javascript.plainenglish.io/nest-js-part-1-creating-your-first-api-71471ac39d3e?source=collection_archive---------4----------------------->

![](img/d2b6fa62684d2afcce32eb8b6ff0dcad.png)

NestJS Tutorial #1: Create Your First API

> 最初发布于—https://www . nandhakumar . io/post/nest-js-tutorial-1-create-your-first-API

你好。👋

与 Nest 合作已经有几个月了。JS 我喜欢这个框架开发可伸缩的服务器端应用的方式

我仍在努力学习更多关于 Nest 的知识。JS，所以想到了以教程系列的形式分享我从初级到高级的学习。

[跟我来](https://medium.com/@nandhakumar.io)会收到这个系列所有即将发布的帖子的通知。

我们现在就开始吧！🚀

# 先决条件

*   [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
*   [打字稿](https://www.typescriptlang.org/)(可选)
*   哎呀的基础
*   [邮递员](https://www.postman.com/)(用于 API 测试)
*   [代码编辑器](https://code.visualstudio.com/)
*   [节点。JS](https://nodejs.org/en/)

# 什么是窝。JS？

巢。JS 是一个构建高度可伸缩节点的框架。JS 服务器端应用。它完全支持 typescript(它也允许我们用纯 JS 构建应用程序)。

它结合了 OOP(面向对象编程)和函数式编程来编写干净和可重用的代码。

如果您曾经构建过服务器端应用程序，您应该听说过 [Express。JS](https://expressjs.com/) 和 [Fastify](https://www.fastify.io/) 库。

引擎盖下，窝。JS 用的是快递。JS 作为它的默认 HTTP 服务器。如果你更喜欢使用 Fastify，你可以很容易地切换[(更多关于这个的官方文档)](https://docs.nestjs.com/first-steps)

这是关于 Nest 的简短介绍。射流研究…

# 生成巢。JS 项目

在生成项目之前，确保您已经安装了最新版本的 Node。您系统上的 JS

我在用 Node。JS 版本`v18.12.1`

来筑巢。JS 项目首先，你需要安装 [Nest Cli](https://docs.nestjs.com/cli/overview)

```
npm i -g @nestjs/cli
```

现在生成一个新的巢。JS 项目

```
nest new [your project name]
```

它会要求，

*   用哪个包经理( [npm](https://www.npmjs.com/) ，[纱](https://yarnpkg.com/)， [pnpm](https://pnpm.io/) )呢？(我选纱，你可以随心选)

现在在代码编辑器中打开项目

# 理解 Nest。JS 项目结构

![](img/10616d7da0f596f317bb203376383712.png)

*   **node_modules** —包含项目所需的所有库。
*   **src** —包含您的应用程序源代码，在这个目录嵌套下。JS 已经生成了一个启动代码。让我们探索它们是什么，
*   **app.controller.spec.ts** —包含每个控制器实现的单元测试用例
*   **app.controller.ts** —包含 [API](https://en.wikipedia.org/wiki/API) 的实现
*   **app.service.ts** —包含将在控制器中使用的业务逻辑
*   **app.module.ts** —包含导入、导出和 DI(依赖注入)。稍后将详细介绍这一点…
*   **main.ts** —包含引导应用程序的实现。这是您的应用程序的起点
*   **测试** —包含 E2E 测试用例实现
*   **.eslintrc.js** —包含 lint 配置，有助于识别不正确的语法、类型脚本标准等…
*   **。gitignore** —包含将代码推送到 GitHub 时要忽略的文件&目录
*   **。prettierrc** —包含更漂亮的配置来格式化你的代码
*   **nest-cli.json** —基础嵌套。JS 配置
*   **package.json** —包含项目所需的依赖项、脚本、项目版本等
*   README.md —包含您项目的文档
*   **tsconfig.json** —包含类型脚本配置

# 对 API 的基本理解(如果你知道什么是 API，你可以跳过这一节)

如果你是一个完全的 API 开发初学者。

简单来说，
假设你有一块布料原料，你想把它缝好。

所以你会去找一个裁缝，把你的衣服拿去缝。你也将给出一些关于设计应该如何的指示。

考虑到上面的例子，在计算机世界中，前端应用程序(具有用户界面的应用程序)将向服务器(裁缝)请求带有一些参数(布料原材料和设计布料的指令)的特定数据，作为回报，服务器将向您发送所请求的数据作为响应(缝制布料)。

这些请求使用 API URL 发送。

一个 API(应用程序编程接口)看起来像这样👇

```
// Example API
"https://google.com/api/users" // returns a list of users
```

如果你还是很困惑。别担心，往前走你会想出办法的。

# 创建您的第一个 API

让我们先启动服务器

打开你的终端

导航到您的项目目录

然后跑

```
yarn start:dev
```

> *将* `*yarn*` *替换为* `*npm*` *或* `*pnpm*` *如果你已经初始配置了那些包管理器*

现在，您的服务器应该已经在

```
http://localhost:3000
```

测试由 Nest 生成的启动代码。射流研究…

Open Postman(测试 API 的工具)

选择**获取**方法并添加**API URL(**[**http://localhost:3000**](http://localhost:3000/)**)**然后点击**发送**

![](img/b458f982ff9542202593ed7b0651f5c4.png)

您将看到响应为“Hello World！”

太好了！

您已经执行了您的第一个 API。

现在让我们试着定制这个 API 来获得一个用户名列表

# 第一步

打开**应用控制器. ts**

*   将**/用户**路线添加到 **@Controller()** 装饰器中
*   将 **@Get()** decorator 下的函数名改为 **getUsers**
*   将返回类型从**字符串**更改为**字符串[]**
*   将应用服务方法名称更改为**获取用户**

代码片段👇

```
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller('/users') // Add '/user' route
export class AppController {
  constructor(private readonly appService: AppService) {}
// Change the function name to getUsers
  @Get()
  getUsers(): string[] { // Change return type to string[](stirng Array) 
     // Change the service method name to getUsers
     return this.appService.getUsers(); 
  }
}
```

# 第二步

打开 **app.service.ts**

*   将 AppService 类中的函数名 **getHello()** 改为 **getUsers()**
*   将返回类型从**字符串**更改为**字符串[]**
*   将返回值从**‘Hello World！’**至`['userOne','userTwo']`

代码片段👇

```
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  // Change function name to getUsers
  getUsers(): string[] { // Change return type to string[](stirng Array) 
    return ['userOne', 'userTwo'];
  }
}
```

就这样，你的用户 API 已经准备好了。

让我们在《邮差》中测试一下

*   开放邮递员
*   选择**获取**方法并添加**API URL(**[**http://localhost:3000/users**](http://localhost:3000/users)**)**然后点击**发送**

![](img/50373256393364bdd240f9fc50b22bba.png)

如果您得到的响应是用户名列表。

恭喜你！👏

你已经在 Nest 中创建了你的第一个 API。射流研究…

从[这里](https://github.com/nandhakumar-rs/nest-js-tutorial-series)获得完整的源代码

# 感谢阅读！

希望你今天学到了新东西😊。

[跟我来](https://medium.com/@nandhakumar.io)获得这个系列所有即将发布的帖子的通知。

在 [Twitter](https://twitter.com/nandhakumar_io) 、 [Instagram](https://www.instagram.com/nandhakumar.io/) 、 [Email](https://mailto:rsnk2013@gmail.com/) 和 [LinkedIn](https://www.linkedin.com/in/nandhakumar-io/) 上关注并联系我，了解更多类似的有趣内容。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***