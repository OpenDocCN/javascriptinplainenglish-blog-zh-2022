# NestJS #2: HTTP 请求和数据验证

> 原文：<https://javascript.plainenglish.io/nest-js-tutorial-2-http-request-data-validation-10c6493de2c9?source=collection_archive---------5----------------------->

![](img/fdbcda5dedaf0cd1ae46d5119048f8b7.png)

Nest JS Tutorial #2: HTTP Request & Data Validation

你好。👋

在这篇文章中，你将学习什么是 HTTP 请求以及如何在 [Nest JS](https://nestjs.com/) 中验证请求数据

如果你不知道什么是 Nest JS，可以看看[我之前的帖子](https://medium.com/javascript-in-plain-english/nest-js-part-1-creating-your-first-api-71471ac39d3e)

> **原帖**—[https://www . nandhakumar . io/post/nest-js-tutorial-2-http-request-data-validation](https://www.nandhakumar.io/post/nest-js-tutorial-2-http-request-data-validation)

# 先决条件

*   [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
*   [打字稿](https://www.typescriptlang.org/)(可选)
*   哎呀的基础
*   [邮递员](https://www.postman.com/)(用于 API 测试)
*   [代码编辑器](https://code.visualstudio.com/)
*   [节点。JS](https://nodejs.org/en/)

# 什么是 HTTP 请求？

HTTP 请求从客户端机器(web 浏览器或任何其他客户端应用程序)发送，以访问服务器或从服务器获取信息。

这些请求是在类似这样的 URL 的帮助下发送的👇

```
https://yourapp.com/api/v1/users
```

## HTTP 请求的三个部分

**方法** —它定义了请求的类型

**Headers** —它将有关于请求和发送者(客户端)的信息，你也可以添加自定义参数。通常情况下，授权 Cookies 会被附加到头部。

**正文** —它将有请求数据。例如，当注册一个新用户时，您必须将用户信息作为请求数据传递，以将其存储在服务器中

## HTTP 请求方法

![](img/8349b42fe994965b1b59284f11d09515.png)

HTTP Request Methods

这是关于 HTTP 请求的简短介绍。

要了解更多 HTTP 请求， [**点击这里！**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

## 为什么请求数据验证？

如您所知，HTTP 请求的主体部分可能包含一些数据。

当 HTTP 请求到达服务器时，不经过验证就直接获取正文数据是不好的。有时你可能会得到恶意数据。因此，要求您始终验证您的请求主体数据。

# 理解 Nest。JS 验证

在巢里。JS，我们有一个叫做验证管道的东西。每当请求主体通过该管道传递并被验证时。如果有任何无效数据，它将抛出一个错误。

**在继续之前，你需要理解什么是 d to(数据传输对象)**

**DTO 是一个你可以定义验证规则的类。如果您对此不确定，请不要担心，在实施时您会明白这一点。**

## 验证管道的两个部分

**类转换器-** 它有助于将你的请求体转换成 DTO 的类实例，然后该实例将被传递给类验证

**类验证器-** 它将根据 DTO 中定义的规则验证请求体，如果有任何无效数据，将抛出一个错误

现在让我们开始实现下面给出的示例场景

**场景:需要添加一个新用户，该用户应该有电子邮件，年龄，姓名和国家(国家是一个可选属性)。**

按照这个场景，很明显我们需要向服务器添加数据

因此，这是一个 HTTP POST 方法，我们需要在请求体中传递用户数据。

希望你已经造了一个窝。JS 项目，如果不是按照我以前的[教程](https://medium.com/javascript-in-plain-english/nest-js-part-1-creating-your-first-api-71471ac39d3e)创建一个。

现在，让我们一步一步地实现，

# 第一步:

在项目中安装类验证器和类转换器

```
npm i class-validator class-transformer -s
```

# 第二步:

生成用户控制器。

```
nest g controller user
```

> **注意:要执行 nest 命令，您应该已经全局安装了
> nest CLI**

# 第三步:

生成用户模块

```
nest g module user/user --flat
```

> **注意:由于我们已经在步骤 2 中创建了一个用户文件夹，
> 为了避免创建额外的文件夹，使用了标志**

# 第四步:

将用户控制器添加到用户模块

```
// user.module.ts
import { Module } from '@nestjs/common';
import { UserController } from './user.controller';
@Module({
  imports: [],
  providers: [],
  controllers: [UserController], // add user controller
})
export class UserModule {}
```

# 第五步:

将用户模块添加到应用模块

```
// app.module.ts
import { Module } from '@nestjs/common';
import { UserModule } from './user/user.module';

@Module({
  imports: [UserModule], // add user module
  controllers: [],
  providers: [],
})
export class AppModule {}
```

# 第六步:

在用户文件夹下创建一个 dto 文件夹，并创建一个名为 user.dto.ts 的文件

![](img/a5f6ba7d796d1b11b82fc5babc022acf.png)

Nest JS Project Structure — User DTO

# 第七步:

*   创建用户到类
*   根据场景将用户属性添加到 UserDTO

```
// user.dto.ts
export class UserDTO {
  email: string;
  age: string;
  name: number;
  country: number;
}
```

# 第八步:

巢。JS 广泛使用[Typescript](https://www.typescriptlang.org/)decorator。

> **注意:** [**装饰者**](https://www.typescriptlang.org/docs/handbook/decorators.html) **是一个简单的函数，帮助修改
> 目标值
> 装饰者的定义类似于** `**@[decoratorname]()**`

回到 UserDTO，

Class-Validator 有一个验证函数列表，可以以装饰器的形式使用

现在，让我们尝试向类属性添加验证装饰器

```
import { IsEmail, IsNumber, IsOptional, IsString } from 'class-validator';

export class UserDTO {
  @IsEmail()
  email: string;

  @IsNumber()
  age: string;

  @IsString()
  name: number;

  // add @IsOptional to make the country property optional
  @IsOptional() 
  @IsString()
  country: number;
}
```

# 第九步:

*   创建一个控制器来添加用户
*   添加 UserDTO 作为请求体的类型

```
import { Body, Controller, Post } from '@nestjs/common';

import { UserDTO } from './dto/user.dto';
@Controller('user')
export class UserController {
  @Post()
  async addUser(@Body() user: UserDTO) {
    return user;
  }
}
```

> *注意:
> 我已经将*[*@ Post*](https://dev.to/post)*Decorator 添加到 addUser 函数中，因为我们>正在处理 Post HTTP 请求
> 同样，@Body Decorator 将获取请求体*

# 第十步:

在 **main.ts** 中全局添加验证管道中间件。通过在全局范围内添加这一功能，它可以帮助 DTO 验证整个应用程序中的数据。

```
// main.ts
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
const CookieSession = require('cookie-session');

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.useGlobalPipes(
    // By adding this validation pipe globally, nest js helps us to validate body params, query param etc..
    new ValidationPipe({
      whitelist: true, // When Whitelist is set to true, You will not be allowed to send additional props apart from DTO Property
    }),
  );

  // Add Cookie Session Middleware to store user id in cookies on the response and the request.
  app.use(
    CookieSession({
      keys: ['SecretKey'],
    }),
  );
  app.listen(3000);
}
bootstrap();
```

就这样，我们在`addUser`请求体中添加了验证

# 测试

现在让我们测试一下实现吧！

通过执行以下命令启动服务器

```
npm start:dev
```

在 [Postman](https://www.postman.com/) 或任何 API 测试工具中打开服务器 URL `http://localhost:3000`

**测试用例 1:**

用无效的电子邮件传递所有用户属性

![](img/4571e48ccadf948c01aa62806c566a5a.png)

Nest.JS Postman Test Case #1

验证成功了！

**测试用例 2:**

由于 country 属性已经设置为可选，现在让我们尝试发送不带 country 属性的请求

![](img/f74543a04580a556ed175d7a9c7f46ea.png)

Nest.JS Postman Test Case #2

现在我们得到了成功的回应，即使没有国家财产。

通过传递无效数据，尝试在不同的场景下进行测试，验证应该会像预期的那样工作

恭喜你！👏

您已成功验证了嵌套中的请求正文。射流研究…

从[这里](https://github.com/nandhakumar-rs/nest-js-tutorial-series)获得完整的源代码

# 感谢阅读！

希望你今天学到了新东西😊。

关注我以获得关于本系列所有即将发布的帖子的通知。

在 [Twitter](https://twitter.com/nandhakumar_io) 、 [Instagram](https://www.instagram.com/nandhakumar.io/) 、 [Email](https://mailto:contact@nandhakumar.io//) 和 [LinkedIn](https://www.linkedin.com/in/nandhakumar-io/) 上关注并联系我，了解更多类似的有趣内容。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***