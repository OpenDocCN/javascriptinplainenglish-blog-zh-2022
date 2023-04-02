# TypeScript 记录类型如何工作

> 原文：<https://javascript.plainenglish.io/how-the-typescript-record-type-works-4f659c1af9ad?source=collection_archive---------9----------------------->

![](img/924d6a8be8b7cf22dd7193efca6af3ff.png)

当尝试实现更复杂的数据类型时，TypeScript 记录是确保一致性的一个好方法。它们强制键值，并允许您为这些值创建自定义接口。

这听起来令人困惑，但让我们看看它在实践中是如何工作的。

# 实用程序类型

记录是一种实用工具类型，这意味着它是一种由 TypeScript 专门定义的类型，用于帮助解决某个问题。

# Typescript 记录类型如何工作

假设您有这样一个数据集:

```
const myData = {
    "123-123-123" : { firstName: "John", lastName: "Doe" },
    "124-124-124" : { firstName: "Sarah", lastName: "Doe" },
    "125-125-125" : { firstName: "Jane", lastName: "Smith" }
}
```

我们的数据集有一个 ID 作为它的键，类型为 string。所有的值都有相同的格式，也就是说，它们有名字和姓氏。

对于这种数据结构，记录是最好的实用类型。我们可以如下定义我们的数据结构类型:

```
type User = {
    firstName: string,
    lastName: string
}const myData:Record<string, User> = {
    "123-123-123" : { firstName: "John", lastName: "Doe" },
    "124-124-124" : { firstName: "Sarah", lastName: "Doe" },
    "125-125-125" : { firstName: "Jane", lastName: "Smith" }
}
```

记录的形式是`Record<K, T>`，其中`K`是键的类型，`T`是值的类型。

上面，我们为我们的值定义了一个新的类型 User，并将我们的键设置为 string 类型。

# 记录类型和联合类型

有时，我们可以有一个对象，它有一组预定义的可能的键。从 API 调用时尤其如此。例如:

```
const myData = {
    "uk" : { firstName: "John", lastName: "Doe" },
    "france" : { firstName: "Sarah", lastName: "Doe" },
    "india" : { firstName: "Jane", lastName: "Smith" }
}
```

让我们假设，对于上面的数据集，键只能是三个值:英国、法国或印度。在这种情况下，我们可以为用户定义一个类型，为键定义一个联合类型:

```
type User = {
    firstName: string,
    lastName: string
}
type Country = "uk" | "france" | "india";const myData:Record<Country, User> = {
    "uk" : { firstName: "John", lastName: "Doe" },
    "france" : { firstName: "Sarah", lastName: "Doe" },
    "india" : { firstName: "Jane", lastName: "Smith" }
}
```

使用这种方法，我们可以对键的允许值以及值应该符合的类型实施严格的规则。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*