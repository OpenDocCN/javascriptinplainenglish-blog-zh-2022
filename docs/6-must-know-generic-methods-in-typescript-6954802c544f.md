# TypeScript 中 6 个必须知道的泛型方法

> 原文：<https://javascript.plainenglish.io/6-must-know-generic-methods-in-typescript-6954802c544f?source=collection_archive---------4----------------------->

## TypeScript 本身提供了几个有用的实用工具类型来帮助我们执行一些常见的类型转换。

![](img/cd29d4ee8c80881ccd7f1551dee1d813.png)

TypeScript 中的类型系统非常强大。它为我们提供了类型安全。虽然类型系统很受欢迎，但如果我们不计划和设计类型和接口，它也会使我们的代码混乱和难以阅读。

TypeScript 本身提供了几个有用的实用工具类型来帮助我们执行一些常见的类型转换。这些实用程序类型是全球可用的，它们都使用泛型，在我们开始之前，让我们简单介绍一下泛型。

## 一般的

避免代码重复和创建可重用类型是编写干净代码的重要部分。泛型是 TypeScript 的一个特性，它允许我们编写可重用的类型。看下面这个例子。

```
type Add<T> = (a: T, b: T) => T

const addNumbers: Add<number> = (a, b) => {
  return a + b
}

const addStrings: Add<string> = (a, b) => {
  return a + b
}
```

将正确的类型放入 Add 的泛型类型中，它可用于描述两个数字的相加或两个字符串的串联。我们不需要为每个函数编写一个类型，只需要用一个泛型类型做一次。这不仅节省了我们的努力，而且使我们的代码更干净，更不容易出错。

有关 TypeScript 泛型的更多信息，可以阅读本文:

[](https://levelup.gitconnected.com/easy-to-master-the-generics-in-typescript-c288e2995bc6) [## 容易掌握 TypeScript 中的泛型

### 为什么我需要一个泛型？

levelup.gitconnected.com](https://levelup.gitconnected.com/easy-to-master-the-generics-in-typescript-c288e2995bc6) 

**以下 7 种实用类型是我们经常使用的。**

## 1.`Partial<Type>`

Partial 构造一个所有类型属性都设置为可选的类型。当我们为一个对象编写更新逻辑时，这非常有用。

```
type User = {
  name: string
  age: number
  address: string
  occupation: string
}

type PartialUser = Partial<User>

// type PartialUser = {
//   name?: string;
//   age?: number;
//   address?: string;
//   occupation?: string;
// }
```

## 2.`Required<Type>`

Required 是 Partial 的反义词。它构造一个类型，该类型的所有属性都是必需的。它可用于确保类型中不出现可选属性。

```
type PartialUser = {
  name: string
  age: number
  address?: string
  occupation?: string
}

type User = Required<PartialUser>

// type User = {
//   name: string;
//   age: number;
//   address: string;
//   occupation: string;
// }
```

## 3.`Pick<Type, Keys>`

选择将从类型中选择属性集键来创建一个新类型。键可以是字符串或字符串的并集。Keys 的值必须是类型的键，否则 TypeScript 编译器会报错。当您希望通过从具有许多属性的对象中拾取某些属性来创建较轻的对象时，该工具类型特别有用。

```
type User = {
  name: string
  age: number
  address: string
  occupation: string
}

type BasicUser = Pick<User, "name" | "age">

// type BasicUser = {
//   name: string;
//   age: number;
// }
```

## 4.省略

`Omit` 与`Pick`相反。键不是关于保留哪些属性，而是要省略的属性键集。当我们只想从对象中删除某些属性而保留其他属性时，这就更有用了。

```
type User = {
  name: string
  age: number
  address: string
  occupation: string
}

type BasicUser = Omit<User, "address" | "occupation">

// type BasicUser = {
//   name: string;
//   age: number;
// }
```

## 5.`Readonly<Type>`

Readonly 构造一个类型，该类型的所有属性都设置为只读。向 TS 重新分配一个新值将会报告一个错误。

```
type User = {
  name: string
  age: number
  address: string
  occupation: string
}

type ReadOnlyUser = Readonly<User>

const user: ReadOnlyUser = {
  name: "Mark",
  age: 34,
  address: "Chicago",
  occupation: "IT Engineer"
}

user.name = "Maxwell"
// Cannot assign to 'name' because it is a read-only property.
```

## 6.`ReturnType<Type>`

ReturnType 从函数类型的返回类型构造类型。当我们处理来自外部库的函数类型并希望基于它们构建自定义类型时，这是非常有用的。

```
import axios from 'axios'

type Response = ReturnType<typeof axios>

function callAPI(): Response{
  return axios("url")
}
```

除了上面提到的，还有其他类型的工具可以帮助我们编写更简洁的代码。可以在这里找到关于实用工具类型的 TypeScript 文档的链接。

[](https://www.typescriptlang.org/docs/handbook/utility-types.html) [## 文档-实用程序类型

### TypeScript 提供了几种实用工具类型来促进常见的类型转换。这些实用程序可用…

www.typescriptlang.org](https://www.typescriptlang.org/docs/handbook/utility-types.html) 

实用工具类型是 TypeScript 提供的一个非常有用的功能。开发人员应该使用它们来避免硬编码类型。想表现的比别人多？这些是你需要知道的。如果你对我的文章感兴趣，可以关注我的[媒](https://hyhwell.medium.com/)。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****