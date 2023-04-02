# 如何构建一个 GraphQL + MongoDB 系列

> 原文：<https://javascript.plainenglish.io/fieldresolver-and-data-loader-made-easy-with-nestjs-part-5-of-how-to-build-a-graphql-mongodb-e0d3d6f7eeec?source=collection_archive---------10----------------------->

## 第 5 部分:使用 NestJS 简化 FieldResolver 和数据加载器

现在您已经有了用 NestJS 构建的带认证的 GraphQL API 是时候讨论数据加载器和批处理了！

![](img/83aa39e8df2668795accfc9f7a4829ae.png)

Photo by ThisIsEngineering: [https://www.pexels.com/photo/female-software-engineer-coding-on-computer-3861972/](https://www.pexels.com/photo/female-software-engineer-coding-on-computer-3861972/)

欢迎回到我的带有 NestJS 系列的 GraphQL！如果你是第一次来这里，请务必阅读我以前的文章:

*   [https://JavaScript . plain English . io/graph QL-nodejs-MongoDB-made-easy-with-nestjs-and-mongose-29 F9 c 0 ea 7 E1 d](/graphql-nodejs-mongodb-made-easy-with-nestjs-and-mongoose-29f9c0ea7e1d)
*   [https://makin hs . medium . com/unit-testing-made-easy-with-nestjs-part-02-for-graph QL-MongoDB-back end-article-series-b37f 147 e2a 9 e](https://makinhs.medium.com/unit-testing-made-easy-with-nestjs-part-02-for-graphql-mongodb-backend-article-series-b37f147e2a9e)
*   [https://makin hs . medium . com/e2e-testing-made-easy-with-nestjs-part-3-of-graph QL-nodejs-MongoDB-series-ba 913 bad 7 cf 2](https://makinhs.medium.com/e2e-testing-made-easy-with-nestjs-part-3-of-graphql-nodejs-mongodb-series-ba913bad7cf2)
*   [https://makin hs . medium . com/authentic ation-made-easy-with-nestjs-part-4-of-how-to-build-a-graph QL-MongoDB-d 6057 EAE 3 fdf](https://makinhs.medium.com/authentication-made-easy-with-nestjs-part-4-of-how-to-build-a-graphql-mongodb-d6057eae3fdf)

很高兴阅读了以前的文章来跟进这篇文章。

我们将讨论一些更高级的 GraphQL 主题，尽管它被认为是某种开发人员(即数据加载者)的基础

我在这里的目标不是判断这个题目有多难，而是展示如何在 NestJS 中使用它。

## GraphQL 和解析器快速回顾

请记住，当我们使用 GraphQL 时，我们可以选择我们想要解析的字段，并且我们还可以有一种方法来解析一个只有在查询中被选择的字段，以防止不必要的数据库查询。

在我们以前的文章中，我们设法创建了一个简单的用户实体，它没有其他需要解析的字段:

```
@Schema()
@ObjectType()
export class User {
  @Field(() => String)
  _id: ***MongooseSchema***.Types.ObjectId | string;
  @Prop()
  @Field(() => String, { description: 'User firstName ' })
  firstName: string;
  @Prop()
  @Field(() => String, { description: 'User lastName ' })
  lastName: string;
  @Prop()
  @Field(() => String, { description: 'User email ' })
  email: string;
  @Prop()
  password: string;
  @Prop()
  @Field(() => String, { description: 'User role' })
  role: string;
}
```

如果我们想把我们的用户链接到一个更详细的地址，可能不止一个地址，会发生什么？

为了实现这一点，我们需要对代码进行一些修改。

让我们开始在 users/entities 文件夹中创建一个地址实体，并创建一个名为`address.entity.ts`的文件。

```
import { ObjectType, Field } from '@nestjs/graphql';
import { Schema as MongooseSchema } from 'mongoose';
import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';

@Schema()
@ObjectType('address')
export class Address {
  @Field(() => String)
  _id: ***MongooseSchema***.Types.ObjectId | string;
  @Prop()
  @Field(() => String, { description: 'Street' })
  street: string;
  @Prop()
  @Field(() => String, { description: 'City' })
  city: string;
  @Prop()
  @Field(() => String, { description: 'State address ' })
  state: string;
  @Prop()
  @Field(() => String, { description: 'ZIP address ' })
  zip: string;
}

export const ***AddressSchema*** = SchemaFactory.*createForClass*(Address);
```

现在，更新我们的 user.entity.ts:

```
import { ObjectType, Field } from '@nestjs/graphql';
import { Schema as MongooseSchema } from 'mongoose';
import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';
import * as mongoose from 'mongoose';
import { Address } from './address.entity';

@Schema()
@ObjectType('user')
export class User {
  @Field(() => String)
  _id: ***MongooseSchema***.Types.ObjectId | string;
  @Prop()
  @Field(() => String, { description: 'User firstName ' })
  firstName: string;
  @Prop()
  @Field(() => String, { description: 'User lastName ' })
  lastName: string;
  @Prop()
  @Field(() => String, { description: 'User email ' })
  email: string;
  @Prop()
  password: string;
  @Prop()
  @Field(() => String, { description: 'User role' })
  role: string;
  @Prop({ type: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Address' }] })
  @Field(() => [Address], { description: 'User addresses' })
  addresses: Array<Address>;
}

export const ***UserSchema*** = SchemaFactory.*createForClass*(User);
```

然后，我们需要在 users.module.ts 中注册它:

```
import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersResolver } from './users.resolver';
import { MongooseModule } from '@nestjs/mongoose';
import { User, ***UserSchema*** } from './entities/user.entity';
import { Address, ***AddressSchema*** } from './entities/address.entity';
import { CommonModule } from '../common/common.module';
import { UsersAddressesResolver } from './users-addresses.resolver';

@Module({
  imports: [
    CommonModule,
    MongooseModule.*forFeature*([
      {
        name: User.name,
        schema: ***UserSchema***,
      },
      {
        name: Address.name,
        schema: ***AddressSchema***,
      },
    ]),
  ],
  providers: [UsersResolver, UsersService, UsersAddressesResolver],
  exports: [UsersService],
})
export class UsersModule {}
```

现在，更新 create-user-input.ts(出于本文的考虑，在其中添加了地址):

```
import { InputType, Field } from '@nestjs/graphql';

@InputType()
export class Address {
  @Field(() => String)
  street: string;
  @Field(() => String)
  city: string;
  @Field(() => String)
  state: string;
  @Field(() => String)
  zip: string;
}

@InputType()
export class CreateUserInput {
  @Field(() => String, { description: 'first name of the user' })
  firstName: string;
  @Field(() => String, { description: 'last name of the user' })
  lastName: string;
  @Field(() => String, { description: 'email of the user' })
  email: string;
  @Field(() => String, { description: 'role of the user' })
  role: string;
  @Field(() => String, { description: 'password of the user' })
  password: string;
  @Field(() => [Address])
  addresses: Array<Address>;
}
```

让我们快速重构构造函数中的 users.service.ts:

```
constructor(
  @InjectModel(User.name)
  private readonly userModel: ***Model***<User>,
  @InjectModel(Address.name)
  private readonly addressModel: ***Model***<Address>,
  private readonly authService: AuthService,
) {}
```

然后`create`功能:

```
async create(createUserInput: CreateUserInput) {
  const saltOrRounds = 10;
  const password = createUserInput.password;
  createUserInput.password = await bcrypt.hash(password, saltOrRounds);
  let addresses = [];
  createUserInput.addresses.forEach((address) => {
    addresses.push((new this.addressModel(address).save()));
  });
  addresses = await ***Promise***.all(addresses);
  const user = new this.userModel({ ...createUserInput, addresses });
  return user.save();
}
```

即使做了这些改变，我们仍然会有一个错误…因为我们仍然需要为地址添加`ResolveField`。为了方便起见，让我们创建一个特定的解析器:

```
nest g resolver users/users-addresses --flat
```

Mongoose 负责处理地址的用户关系。我们应该已经有了地址 id，所以我们的解析器应该简单如下:

```
import { Parent, ResolveField, Resolver } from '@nestjs/graphql';
import { InjectModel } from '@nestjs/mongoose';
import { Address } from './entities/address.entity';
import { ***Model*** } from 'mongoose';
import { User } from './entities/user.entity';

@Resolver(() => User)
export class UsersAddressesResolver {
  constructor(
    @InjectModel(Address.name)
    private readonly addressModel: ***Model***<Address>,
  ) {}

 @ResolveField('addresses', () => [Address])
 async getUserAddresses(@Parent() user: User) {
   return this.addressModel
    .find({
       _id: { $in: user.addresses },
     })
     .exec();
 }
}
```

这应该是好的去！

让我们运行`yarn start`并在操场上测试我们的变化:[http://localhost:3000/graph QL](http://localhost:3000/graphql)

```
mutation CreateUser($createUserInput: CreateUserInput!) {
  createUser(createUserInput: $createUserInput) {
    _id
    firstName
    lastName
    email
    addresses{
      street
    }
  }
}
```

然后是变量:

```
{
  "createUserInput":{
    "email":"[tio.makin+medium4@gmail.com](mailto:tio.makin+medium4@gmail.com)",
    "password":"medium!23",
    "firstName": "marcos",
    "lastName": "silva",
    "role": "admin",
    "addresses": [
      {
      "street": "fake street 1",
      "city": "curitiba",
      "state": "pr",
      "zip": 81630130
      },

      {
      "street": "fake street 2",
      "city": "curitiba",
      "state": "pr",
      "zip": 81630130
      }
    ]
  }
}
```

登录以获取访问令牌:

```
mutation LoginUser($loginCredentials:LoginUserInput!){
  loginUser(loginUserInput:$loginCredentials){
  access_token
  }
}
```

变量:

```
{
  "loginCredentials": {
    "email": "[tio.makin+medium5@gmail.com](mailto:tio.makin+medium5@gmail.com)",
    "password": "medium!23"
  }
}
```

获取 access_token，然后，为了简单起见，获取所有用户:

```
query ListUsers($args:ConnectionArgs!){
  listUsersWithCursor(args: $args) {
    page {
      edges {
        node {
          _id
          firstName
          lastName
          email
          role
          addresses{
            street
          }
        }
      }
      pageInfo {
        startCursor
        endCursor
        hasPreviousPage
        hasNextPage
      }
    }
  }
}
```

HTTP 头变量:

```
{
  "Authorization":"Bearer ADD_HERE_YOUR_ACCESS_TOKEN_WITH_BEARER"
}
```

您的结果应该类似于:

```
{
  "data": {
    "listUsersWithCursor": {
      "page": {
        "edges": [
          {
            "node": {
              "_id": "630d26de625c1256b8deb6ed",
              "firstName": "marcos",
              "lastName": "silva",
              "email": "[tio.makin+medium5@gmail.com](mailto:tio.makin+medium4@gmail.com)",
              "role": "admin",
              "addresses": [
                {
                  "street": "fake street 1"
                },
                {
                  "street": "fake street 2"
                }
              ]
            }
          }
        ],
        "pageInfo": {
          "startCursor": "YXJyYXljb25uZWN0aW9uOjA=",
          "endCursor": "YXJyYXljb25uZWN0aW9uOjA=",
          "hasPreviousPage": false,
          "hasNextPage": false
        }
      }
    }
  }
}
```

现在我们终于有了开始这篇文章的一切！问题已经设置好了，您可能很好奇，想通过添加更多用户并调用相同的用户查询列表来测试它，尤其是控制台记录 ResolveField…将会发生的是，对于每个用户,“addresses”的@ResolveField 将被调用，对于我们编写的内容，我们将为每个找到的用户调用 mongose find 函数。

也就是说，在简历中:

*   数据库中有一个用户，我们有一个地址调用
*   数据库中有两个用户，我们有两个地址调用
*   有 3 个-> 3 个
*   有 N -> N

因此，这会导致 N+1 问题

*“当数据访问框架执行 N 条额外的 SQL 语句来获取在执行主 SQL 查询时本可以检索到的相同数据时，就会出现 N+1 查询问题。”(* [*参考*](https://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem-in-orm-object-relational-mapping) *)*

现在，我们如何组合 FieldResolver 以避免不必要的数据库调用呢？使用数据加载器！

## 数据加载器的用途和优点

带有 [dataloader](https://www.npmjs.com/package/dataloader) 库的 NestJS 允许我们一次解析额外的字段，最大限度地减少对数据库的过多查询。简而言之，它允许我们控制何时调用数据库查询(或外部 API，或您需要做的任何事情)。

首先，让我们用以下代码添加[数据加载器](https://www.npmjs.com/package/dataloader)库:

```
yarn add dataloader
```

基于 NestJS 文档，让我们为数据加载器创建一个提供者:

```
nest g provider users/data-loader/addresses-from-user.loader
```

它应该在用户内部创建一个名为`data-loader`的文件夹和“addresses-from-user.loader.ts”文件:

在这里，我们必须更改请求范围:

```
import { Injectable, Scope } from '@nestjs/common';

@Injectable({ scope: Scope.*REQUEST*})
export class AddressesFromUserLoader {}
```

现在，在构造函数内部，我们需要设置我们想要使用来自 MongoDB 的地址模型，并设置要使用的函数:

```
constructor(
  @InjectModel(Address.name)
  private readonly addressModel: ***Model***<Address>,
) {
  super((keys) => this.batchLoad(keys));
}
```

**batchLoad** 是我们正在扩展的数据加载器中已经存在的一个函数。batchLoad 还接收我们需要设置的 id 数组，这些 id 已经由 NestJS 排序。

一个简单的实现是:

```
private async batchLoad(userAddresses: readonly string[]): Promise<ArrayLike<Address>> {
  const addresses = await this.addressModel
    .find({
      _id: { $in: userAddresses },
    })
    .exec();

  const parsedResults = [];
  for (let i = 0; i < userAddresses.length; i++) {
    const addressesId = userAddresses[i];
    parsedResults.push(addresses.find(({ id }) => id === addressesId));
  }
  return parsedResults;
}
```

我们基本上做的是接收一个地址 id 数组，只调用一次 Mongoose，然后将结果过滤到一个与接收到的订单相匹配的数组中。

> **免责声明**:这可能不是提取地址并进行过滤的最佳方式。暂时为了继续写这篇文章，我仓促地采用了这个解决方案。

既然我们已经设置了数据加载器，我们需要通过调用数据加载器来重构**users-addresses . resolver . ts**文件中的 UsersAddressesResolver。

首先将构造函数改为:

```
constructor(private readonly addressesFromUserLoader: AddressesFromUserLoader) {}
```

然后重构我们的 getUserAddresses 函数:

```
@ResolveField('addresses', () => [Address])
async getUserAddresses(@Parent() user: User) {
  return this.addressesFromUserLoader.loadMany(user.addresses.toString().split(','));
}
```

最终文件应该是:

```
import { Parent, ResolveField, Resolver } from '@nestjs/graphql';
import { Address } from './entities/address.entity';
import { User } from './entities/user.entity';
import { AddressesFromUserLoader } from './data-loader/addresses-from-user.loader';

@Resolver(() => User)
export class UsersAddressesResolver {
  constructor(private readonly addressesFromUserLoader: AddressesFromUserLoader) {}

  @ResolveField('addresses', () => [Address])
  async getUserAddresses(@Parent() user: User) {
    return this.addressesFromUserLoader.loadMany(user.addresses.toString().split(','));
  }
}
```

> **免责声明** *:你可以检查我们是否使用了一个名为 **loadMany** 的函数，因为在我们的研究案例中，一个用户可以有不止一个地址。如果您只需要使用一个不是数组的字段，请使用 **load** 函数。

基本就是这样！我们准备再次测试。在我的测试场景中，我添加了 3 个用户，并为每个用户添加了 2 个地址:

![](img/5ca2685ca702fb8e67aee5d394a77151.png)

Users with addresses

![](img/4192e9435eddea05c8e2bb28a4fbbc04.png)

Address sample from the database

现在调用与之前相同的用户列表查询:

```
query ListUsers($args:ConnectionArgs!){
  listUsersWithCursor(args: $args) {
    page {
      edges {
        node {
          _id
          firstName
          lastName
          email
          role
          addresses{
            _id
            street
            state
            zip
          }
        }
      }
      pageInfo {
        startCursor
        endCursor
        hasPreviousPage
        hasNextPage
      }
    }
  }
}
```

![](img/0260ee5def914a85f70132c284ebc217.png)

query to list users

您将会看到一切工作正常，但是如果我们记录我们的 **getUserAddresses** 字段解析器和 **batchLoad** 函数，我们可以看到以下内容:

*   字段解析器不断被找到的用户数量调用。

```
Received addresses field to resolve [
  new ObjectId("630dd2f7fc39b866ee88eb2b"),
  new ObjectId("630dd2f7fc39b866ee88eb2c")
]
Received addresses field to resolve [
  new ObjectId("630dd308fc39b866ee88eb31"),
  new ObjectId("630dd308fc39b866ee88eb32")
]
Received addresses field to resolve [
  new ObjectId("630d26de625c1256b8deb6e9"),
  new ObjectId("630d26de625c1256b8deb6ea")
]
```

*   **batchLoad** 函数只被调用一次，接收所有要查找的 id:

```
received address to find [
  '630dd2f7fc39b866ee88eb2b',
  '630dd2f7fc39b866ee88eb2c',
  '630dd308fc39b866ee88eb31',
  '630dd308fc39b866ee88eb32',
  '630d26de625c1256b8deb6e9',
  '630d26de625c1256b8deb6ea'
]
```

因此，现在我们不是对我们发现的每个用户调用我们的数据库，而是组合所有的 id，只调用我们的数据库一次来查找用户地址！

在本文中，我展示了如何使用 [**ResolveField**](https://docs.nestjs.com/graphql/resolvers#query-type-names) 以及如何向其添加 [**dataloader**](https://www.npmjs.com/package/dataloader) 。

给出的例子可能很愚蠢，但这里的主要挑战是找到一个简单的例子，并展示如何应用它。

在实际工作中，您可能会发现自己处于类似的情况，但是需要调用外部 API 来获取所需的字段，例如连接到不同的数据库，或者连接到不同的微服务。在这种情况下，调用次数总是会成为一个严重的问题，数据加载器方法将帮助您解决这个问题

我希望这篇文章对您在 NestJS 中的 GraphQL 知识有所帮助。这个项目的源代码可以在这个[链接](https://github.com/makinhs/nestjs-with-graphql/tree/005-data-loader)中找到。

以下是一些值得继续阅读的有用文章:

[](https://makinhs.medium.com/a-beginner-introduction-to-algorithms-and-complexity-with-javascript-typescript-2c8fd2384a1f) [## Javascript/Typescript 算法和复杂性入门

### 通过这篇关于算法和复杂性的介绍性文章，让您的 Javascript/Typescript 技能更上一层楼！

makinhs.medium.com](https://makinhs.medium.com/a-beginner-introduction-to-algorithms-and-complexity-with-javascript-typescript-2c8fd2384a1f) [](https://makinhs.medium.com/how-to-apply-solid-principles-with-typescript-in-an-easy-way-b91b53bc9853) [## 如何以简单的方式应用 Typescript 的坚实原理

### 在本文中，我们将讨论坚实的原则以及如何在您的 Typescript 项目中使用它！

makinhs.medium.com](https://makinhs.medium.com/how-to-apply-solid-principles-with-typescript-in-an-easy-way-b91b53bc9853) 

感谢阅读，如果这篇文章对你有用，别忘了鼓掌 / **评论**！

下一集再见，

干杯

> *如果这类文章过于简单，而你又觉得自己准备了一次真正的冒险，特地在一个遥远的好报酬的基础上，请尝试加入* [*Toptal*](https://topt.al/KncQD8) *与我的引荐* [*链接*](https://topt.al/KncQD8)*[*https://topt.al/KncQD8*](https://topt.al/KncQD8)*。Toptal 是一个伟大的自由职业者社区，我很高兴在那里见到你！**

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。**