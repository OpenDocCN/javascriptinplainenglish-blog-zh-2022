# 如何在 TypeScript 中正确使用自定义类型？

> 原文：<https://javascript.plainenglish.io/how-to-use-custom-types-properly-in-typescript-4df4894d016b?source=collection_archive---------8----------------------->

## 在 TypeScript 中掌握自定义数据类型

![](img/be510b12a627077d26de0df8dd548a48.png)

Photo by [Tianyi Ma](https://unsplash.com/@tma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 不是一种强类型语言。而 TypeScript 是强类型的，这意味着任何东西都有类型，无论是变量还是函数。

有时候，我们想让一个对象具有特定的格式，或者让一个函数返回特定的格式。这是我们在 TypeScript 中使用自定义类型的地方，因为它允许我们定义自己的自定义类型，然后我们可以在代码中使用这些类型。

# 为什么我们需要使用自定义类型？

假设您有一个使用 API 获取数据的函数，并且总是以某种格式返回数据。如果 API 以错误的格式返回数据，我们可能不希望错误格式的数据出现在我们的代码中，因为这会导致问题。在这种情况下，我们可能需要函数的返回是某种类型的。那时我们将定义我们自己的类型。

# 别名类型(使用 type 关键字)

别名类型是如何创建类型的一个例子。以下是我们如何定义自定义类型的示例:

```
type *Person* = {
    name: string,
    address: string,
    age?: number
}
```

如果我们给定类型为`Person`的东西，那么我们期望它至少有一个 ***名称*** 和 ***地址*** ，以及一个可选的 ***年龄*** ，这不是必须给定的。正如你所看到的，在我们的类型中有一个问号表示这个属性是可选的。

如果我们要在代码中使用它，我们可能会这样做:

```
let *getPerson* = async function(): Promise<Person> {
    let getApi = await *fetch*('/api/data', {
        method: 'GET'
    })
    let getResult:Person = await getApi.*json*();
    return getResult;
}
```

在上面的代码中，我们返回了一个类型为 **Person** 的承诺，如果我们没有得到，我们将得到一个错误。例如，如果我们试图运行这个程序，但是我们没有从我们的 API 得到一个地址或名称，我们将会有一个可以处理的错误。

# 扩展别名类型

TypeScript 中有一个选项，您可以在其中扩展先前定义的别名类型。在某些情况下，您可能希望在需要添加不同属性的地方拥有另一个子类型。例如:

```
type *Person* = {
    name: string,
    address: string,
    age?: number
}type *Employee* = Person & {
    company: string
}
```

在上面的例子中，Employee 将拥有 Person 拥有的一切，外加一个名为 company 的必需属性。

# 改为使用接口(使用 interface 关键字)

到目前为止，我们所说的一切都使用了`type`关键字，但是我们可以使用`interface`关键字来代替。

用哪个真的是个人喜好。我们上面的例子看起来像这样，带有`interface`:

```
interface *Person* {
    name: string,
    address: string,
    age?: number
}interface *Employee* extends *Person* {
    company: string
}
```

# 工会类型

有一种更简单的语法叫做联合类型来定义自定义类型。假设我们有一个类型，要么是字符串，要么是数字，叫做 myType。这在我们有可能是字符串或数字的数据的情况下很有用。我们可以定义如下所示类型:

```
type *myType* = number | string
```

# 文字类型

有些情况下，一个变量可能只有一个特定的值列表。在这些情况下，我们可以使用定义的值列表作为类型。

就说我们原来的类型，`AddressType`只能有三个值，家，办公室，或者其他。我们可以定义一个文字类型，并使用它作为我们的`addressType`属性的类型:

```
type *AddressType* = "home" | "office" | "other" 
type *Person* = {
    name: string,
    address: string,
    addressType: AddressType,
    age?: number
}
```

# 结论

创建自定义类型来表示在您自己的代码中使用的数据结构可能非常有用，并将为您的项目提供灵活性。除了从整体上增加您自己代码的类型安全性之外，拥有您自己的类型肯定会改善您与队友在同一代码库上工作时的开发人员体验。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***