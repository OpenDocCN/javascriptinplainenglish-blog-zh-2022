# 6 种最有用的类型脚本实用工具类型

> 原文：<https://javascript.plainenglish.io/6-most-useful-typescript-utility-types-9cace01a62b5?source=collection_archive---------7----------------------->

## 6 种最有用的 TypeScript 实用工具类型，将帮助您编写更好的代码

![](img/3b5cdd38b490d613c8b998d717f220ae.png)

我从事 TypeScript 工作已经快一年了，在这段时间里，我学到了很多，也实现了很多。其中，我最喜欢的 typescript 是允许我编写更好的代码的实用程序类型，所以今天我将讨论 6 种最有用的实用程序类型，它们将帮助您编写更好的代码。

让我们开始吧:

# 记录

如果你想用类型`types`的一组属性`keys`构造一个对象类型，那么记录是最好的实用类型。

## 例子

你想创建一个对象类型来存储用户的信息，这里你可以使用`Record`工具来实现同样的目的。

```
// Our user ID will be a string
type UserID = string// Defining our available user information types
type UserInfo = {
  name: string;
  email: string;
  avatarUrl: string;
}const users: Record<UserID, UserInfo> = {
 "uuid1": { "name": "user1", "email": "[user1@gmail.com](mailto:user1@gmail.com)", "avatarUrl": "[https://user1.com/avatar.png](https://user1.com/avatar.png)" },
 "uuid2": { "name": "user2", "email": "[user2@gmail.com](mailto:user2@gmail.com)", "avatarUrl": "[https://user2.com/avatar.png](https://user2.com/avatar.png)" },
 "uuid3": { "name": "user3", "email": "[user3@gmail.com](mailto:user3@gmail.com)", "avatarUrl": "[https://user3.com/avatar.png](https://user3.com/avatar.png)" }
 }
```

*如果试图添加* `*UserInfo*` *类型中不存在的任何其他类型，TypeScript 会给出编译错误。*

# 部分的

当您希望使用现有类型，但希望所有属性都是可选的时，Partial 实用程序类型非常有用。

## 例子

假设您想要更新用户的一个属性，并且您已经有了一个包含所有必需属性的用户界面，但是您不想创建一个单独的界面来更新用户信息。使用分部实用程序，您可以动态创建一个所有属性都可选的类型。

```
// User interface with all required properties
interface User{
 id:string;
 name: string;
 slug: string;
 group: string[];
 avatarUrl: string;
 about: string;
}// Partial<User> generates a new type based on User with all the property
// keys being optional
const updateUser: Partial<User> = {
  about: 'I am a software engineer.'
}
```

# 需要

Required 实用程序类型与 Partial 实用程序类型正好相反，当您希望使用现有类型但希望所有属性都是必需的时，它非常有用。

## 例子

在某些情况下，您可能希望强制一个对象具有所有必需的属性，即使原始类型将其中一些属性定义为可选的。

```
// User type has lastName property as optional
type User = {
    firstName: string,
    lastName?: string
}// You want to create a user with both firstName and lastName, so you can use User type with Required utility type to make all the properties as required.
const user1: Required<User> = {
    firstName: "John",
    lastName: "Doe"
}
```

# 省略

省略实用程序类型可用于通过省略另一个对象类型的特定属性来创建对象类型。

## 例子

假设您有一个具有某些属性 X、Y 和 Z 的对象类型用户。如果您想要创建一个没有属性 Z 的对象类型，那么您可以使用此实用程序类型。

```
type Product = {
  X: string;
  Y: string;
  Z: string;
}type ProductWithoutZ = Omit<Product, "Z">;
```

# 挑选

使用 Pick 实用程序类型，可以从现有类型中拾取属性来创建新类型。当您的子组件与父组件有一些共同的属性时，您可以通过选择这些属性为子组件创建一个类型。

## 例子

```
type ParentType = {
  X: string;
  T: number;
  S: boolean;
}type ChildType = Pick<ParentType, "X" | "S">
```

# 排除

当使用联合类型时，通常情况下，您希望将联合类型仅用于某些成员，而不是所有成员，在这种情况下，您可以使用排除实用程序来实现相同的目的。

## 例子

```
type ReactionUnion = '👍' | '👎' | '😄' |  '🎉' | '😕' | '❤️' | '👀' | '🚀'// This is equivivalent to  '👍' | '👎' 
type OnlyThumbsUnion = Exclude<ReactionUnion , '😄' |  '🎉' | '😕' | '❤️' | '👀' | '🚀'>
```

# 摘要

在本文中，我们讨论了 6 种 typescript 实用工具类型，它们将帮助您编写更好的 TypeScript 代码。TypeScript 提供了更多的实用程序类型，你可以在这里查看它们。

这个话题到此为止。感谢您的阅读。

# 与我联系

[LinkedIn](https://www.linkedin.com/in/sachin-chaurasiya) | [Twitter](https://twitter.com/sachindotcom)

*原发布于*[*https://blog . sachinchurasiya . dev*](https://blog.sachinchaurasiya.dev/typescript-utility-types-the-6-most-useful)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***