# NestJS #3:查询和路由参数

> 原文：<https://javascript.plainenglish.io/nestjs-tutorial-query-route-params-221cc8000518?source=collection_archive---------3----------------------->

## 了解什么是路由和查询参数，何时使用以及如何在 NestJS 中使用

![](img/25efa725656fa8b20ab8c485cb7b2425.png)

Nest JS Tutorial #3 : Query & Route Params

# 你好。👋

在这篇文章中，你将学习什么是路由和查询参数，什么时候使用它，以及如何在[嵌套 JS](https://nestjs.com/) 中使用它

这篇文章是 nest js 教程系列的一部分，请查看我在 Nest JS 上的另一篇文章以了解更多。

> ***原帖于****——*[https://www . nandhakumar . io/post/nest-js-tutorial-3-route-and-query-param](https://www.nandhakumar.io/post/nest-js-tutorial-3-route-and-query-param)

# 先决条件

*   [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
*   [打字稿](https://www.typescriptlang.org/)(可选)
*   哎呀的基础
*   [邮递员](https://www.postman.com/)(用于 API 测试)
*   [代码编辑器](https://code.visualstudio.com/)
*   [节点。JS](https://nodejs.org/en/)

# 了解路线和查询参数

## 路线参数

路由参数用于获取特定数据。

示例场景，
假设您想要通过`ID`获取用户详细信息，那么`ID`可以像这样作为路由参数传递👇

```
http://api.com/5689
```

这里，`5689`是用户的`ID`

## 查询参数

当您想要对数据进行过滤、排序和分页时，可以使用查询参数。

示例场景，
假设您想要获取一个与姓名匹配的用户列表。因此，这里的 name 可以像这样作为查询参数传递👇

```
http://api.com?name=tamilan
```

这里，名字`tamilan`作为查询参数传递。以获得与名称匹配的结果。

您也可以传递多个查询参数。

除了按名称过滤之外，我们还可以使用现有的名称查询添加一个排序查询，如下所示👇

```
http://api.com?name=tamilan&sort=name
```

这是关于路由和查询参数的简短介绍！

现在让我们看看如何在嵌套 js 中捕获这些查询和路由参数

# 在嵌套 JS 中使用路由和查询参数

首先，使用 nest cli 创建一个新的 nest 项目。如果你不确定如何创建一个新项目，看看这个[帖子](https://medium.com/javascript-in-plain-english/nest-js-part-1-creating-your-first-api-71471ac39d3e)

我已经创建了一个新的 nest 项目，并提供了启动代码。

这是我现在的项目结构，

![](img/1d3449c5cbf65688b7e504a69eeca79a.png)

Nest JS Starter Project Structure

# 要求

我们需要两条路线，

`/user`

*   这应该是一个 GET 请求
*   当没有查询参数时，它应该返回所有用户
*   当名称查询参数被传递时，它应该返回与名称匹配的所有用户

`/user/:id`

*   这应该是一个 GET 请求
*   它应该返回与作为路由参数传递的 id 相匹配的用户

# 履行

## 第一步:

向服务文件添加一些模拟用户数据。

因为我们使用的是 typescript，所以为用户添加一个界面会很好。

```
// app.service.ts

import { Injectable } from '@nestjs/common';

// user interface
export interface IUser {
  id: number;
  name: string;
  age: number;
}

@Injectable()
export class AppService {
  // list of users
  private users: IUser[] = [
    {
      id: 1,
      name: 'Tamilan',
      age: 23,
    },
    {
      id: 1,
      name: 'Nandha',
      age: 24,
    },
    {
      id: 1,
      name: 'Nandha Kumar',
      age: 24,
    },
  ];
}
```

## 第二步:

创建一个方法`findUsersByName`,当没有名称查询时，返回匹配“名称”查询的用户或所有用户。

将此方法添加到同一个服务文件中

```
findUsersByName(nameToBeMatched: string): IUser[] {
    return nameToBeMatched
      ? this.users.filter((user) =>
          // return users with name matching
          // 'name' query param
          user.name.toLowerCase().includes(nameToBeMatched),
        )
      : // returns all the users if the
        // 'name' query param is 'null' or ''
        this.users;
  }
```

## 第三步:

创建另一个方法`findUserById`,返回一个匹配‘id’路由参数的用户

将此方法添加到同一个服务文件中

```
findUserById(id: string): IUser {
    // return user with id matching 'id' route param

    // By Default when you get value from query or route
    // param it will be string, But in our case user id is of
    // type number. So we are making a type conversion for id
    return this.users.find((user) => user.id === Number(id));
  }
```

## 第四步:

将控制器的基本路线更新为`/user`

```
import { Controller, Get} from '@nestjs/common';
import { AppService, IUser } from './app.service';

@Controller('/user') // update the base route to '/user'
export class AppController {
  constructor(private readonly appService: AppService) {}

}
```

## 第五步:

实现需求的第一部分。

用`@Get()`装饰器创建一个方法`getUsers`。

并且它应该以`@Query()` decorator 作为它的参数。因此，每当我们向 URL 添加查询时，这些参数都将被该参数捕获。

在实现中，将查询参数传递给我们已经在服务中实现的服务方法(`findUsersByName`)

最后，返回数据

```
import { Controller, Get} from '@nestjs/common';
import { AppService, IUser } from './app.service';

@Controller('/user')
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getUsers(@Query() params: any): IUser[] {
    return this.appService.findUsersByName(params.name);
  }
}
```

**亲提示**

如果您想从查询中得到一个特定的属性，您可以在`@Query()`装饰器中指定属性`name`，如下所示👇

```
@Get()
  getUsers(@Query('name') name: string): IUser[] {
    return this.appService.findUsersByName(name);
  }
```

## 第六步:

实现需求的第二部分。

用`@Get(':id')`装饰器创建一个方法`getUserById`。

> ***注:*** *这里我们已经定义了:* `*@Get()*` *中的 id' route param '装饰器。*

并且它应该以`@Param()` decorator 作为它的参数。因此该参数将捕获路由参数。

在实现中，将查询参数传递给我们已经在服务中实现的服务方法(`findUserById`)

最后，返回数据

```
import { Controller, Get, Param, Query } from '@nestjs/common';
import { AppService, IUser } from './app.service';

@Controller('/user')
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getUsers(@Query() params: any): IUser[] {
    return this.appService.findUsersByName(params.name);
  }

  @Get(':id')
  getUserById(@Param() params: any): IUser {
    return this.appService.findUserById(params.id);
  }
}
```

**亲提示**

类似于`@Query()`装饰器，您可以像这样在`@Param()`装饰器中指定属性`id`👇

```
@Get()
  getUsers(@Param('id') id: string): IUser {
    return this.appService.findUsersByName(id);
  }
```

就是这样！

根据需求，您已经实现了 API。

# 测试

现在让我们测试一下实现吧！

通过执行以下命令启动服务器

```
npm run start:dev
```

在 [Postman](https://www.postman.com/) 或任何 API 测试工具中打开服务器 URL `http://localhost:3000`

## **测试用例 1:**

获取所有用户，不带查询参数

![](img/d9963bf017b2c48b1de2be94cf7da8a0.png)

Nest JS Query and Route Param, Test Case — 1

我们得到了所有的用户。

✅测试案例通过！

## **测试用例 2:**

使用`name`查询参数获取所有用户

![](img/723022388653517b6339fe8a274cd8dd.png)

Nest JS Query and Route Param, Test Case — 2

我们得到了与查询参数中传递的名称相匹配的所有用户。

✅测试案例通过！

## **测试用例 3:**

使用 id 和`id`路线参数获取用户

![](img/ac09560fcb0ab914cb086e8959613071.png)

Nest JS Query and Route Param, Test Case — 3

我们得到了在路由中传递的用户 id

✅测试案例通过！

尝试用多个`Query`和`Route`参数实现不同的场景。

恭喜你！👏

您已经在 Nest 中成功实现了带有`Query`和`Route`参数的 API。射流研究…

从[这里](https://github.com/nandhakumar-rs/nest-js-tutorial-series)获取完整的源代码。

# 感谢阅读！

希望你今天学到了新东西😊。

[关注我](https://medium.com/@nandhakumar.io)获得本系列所有即将发布的帖子的通知。

在 [Twitter](https://twitter.com/nandhakumar_io) 、 [Instagram](https://www.instagram.com/nandhakumar.io/) 、 [Email](https://mailto:contact@nandhakumar.io/) 和 [LinkedIn](https://www.linkedin.com/in/nandhakumar-io/) 上关注并联系我，了解更多类似的有趣内容。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***