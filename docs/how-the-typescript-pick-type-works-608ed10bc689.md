# TypeScript Pick 类型如何工作

> 原文：<https://javascript.plainenglish.io/how-the-typescript-pick-type-works-608ed10bc689?source=collection_archive---------10----------------------->

![](img/6ed541888628d711afcb2bde4eb93284.png)

TypeScript `Pick`类型是一种实用类型，用于基于现有类型创建新的自定义类型。与[省略型](https://fjolt.com/article/typescript-omit-type)相反。让我们看看它是如何工作的。

# 自定义类型

我们在本指南中使用自定义类型。如果你是定制类型的新手，[在这里查看我的定制类型指南](https://fjolt.com/article/typescript-creating-custom-types)。

# 类型脚本选择实用程序类型

TypeScript 有许多实用工具类型，它们本质上是解决特定问题的自定义类型。`Pick`解决的问题是当我们有一个已经存在的类型，并且想仅仅使用该类型的几个字段来创建一个新的类型。例如，假设我们有一个看起来像这样的`User`类型:

```
type User = {
    firstName: string,
    lastName: string,
    age: number
}
```

在代码的另一部分，我们想要引用一个用户，但是我们知道数据只给出名字和姓氏。因此，我们实际上不能使用`User`类型，因为所有字段都是必需的。如果我们想基于`User`创建一个新类型，我们可以使用`Pick`。

`Pick`有两个参数，第一个是`Type`，这是我们想要使用的类型，第二个是**联合类型**或我们想要从我们正在使用的类型中选择的字段列表。我们这样写:`Type&lt;User, "fields" | "to" | "include">`。例如，让我们制作一个只有`firstName`和`lastName`的新类型:

```
type User = {
    firstName: string,
    lastName: string,
    age: number
}
type UserName = Pick<User, "firstName" | "lastName">
```

现在，使用我们的新类型`UserName`，我们可以定义一个只包含`firstName`和`lastName`的变量:

```
let user:UserName = {
    firstName: "John",
    lastName: "Doe"
}
```

如果我们想创建一个新的类型，它只包含用户的年龄，我们也可以使用`Pick`。下面是一个例子:

```
type User = {
    firstName: string,
    lastName: string,
    age: number
}type UserAge = Pick<User, "age">let age:UserAge = {
    age: 1534
}
```

如您所见，`Pick`类型在基于现有类型创建定制类型时非常有用。现在您已经掌握了它，您可以简化您的类型声明。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*