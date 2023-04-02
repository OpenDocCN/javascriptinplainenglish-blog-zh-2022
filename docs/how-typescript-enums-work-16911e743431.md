# 类型脚本枚举如何工作

> 原文：<https://javascript.plainenglish.io/how-typescript-enums-work-16911e743431?source=collection_archive---------14----------------------->

![](img/4d4a2c48a839f6f0e47cc4a0632ef6d6.png)

Enums 是 Enumerations 的缩写，是预设的常量，可以由开发人员定义，用于代码中的其他地方。

对于 JavaScript 开发人员来说，枚举的概念通常是新的，但是它们相对容易理解。列举给我们写的东西增加了上下文。

# 如何定义枚举

枚举可以在 TypeScript 中使用 **enum** 关键字来定义。这里有一个例子:

```
enum Pet {
    Dog,
    Cat,
    Goldfish,
    Skeleton
}
```

默认情况下，将为其中的每一项分配一个值。所以狗会是 0，猫是 1，以此类推。假设我们有一个产生宠物的函数。以前，我们可能会这样写:

```
// Generate a Cat
generatePet(1);
```

现在，我们可以将上下文添加到我们正在做的事情中，并使用我们的枚举列表来做到这一点:

```
// Generate a Cat
generatePet(Pet.Cat);
```

上面的代码等同于我们之前所做的，只是我们使用了枚举来代替。

# 所以等等…为什么要用枚举？

你可能会想，“这有什么意义？”这是一个合理的问题。枚举本质上允许我们给我们正在做的事情更多的上下文。我们可以要求用户使用 Enum 列表，而不是让用户记住一系列可能的宠物编号。这也给了下一个阅读我们代码的人一个更好的想法，知道我们在做什么。

# 数字和字符串枚举

我们可以将枚举定义为数字或字符串。让我们稍微详细地看看这些。

```
enum Pet {
    Dog = 2,
    Cat,
    Goldfish,
    Skeleton
}
```

上面，我们给了 Dog 一个数值 2。之后的每一项都会增加 1，所以猫变成了 3，金鱼变成了 4，等等，但是你也可以随意定义它们:

```
enum Pet {
    Dog = 2,
    Cat = 9,
    Goldfish = 15,
    Skeleton = 44
}
```

通常我们不会混合字符串和数字以避免混淆，但是我们也可以将枚举完全定义为字符串:

```
enum Counting {
    One = "one",
    Two = "two",
    Three = "three"
}
```

# 函数的枚举值

枚举也可以是返回值的函数。如果在一个枚举中只定义一个值，函数必须放在末尾。如果你把函数放在开头，那么所有的枚举都需要值。因此，下面将引发一个错误:

```
// This will throw an error, since the function is at the start
// So typescript assumes all will be functions
enum Counting {
    One = getOne(),
    Two,
    Three,
}
```

但这不会:

```
enum Counting {
    One,
    Two,
    Three = getThree(),
}
```

上面一个返回`0`，`Two`返回`1`，三个返回`getThree()`的值。举个例子，我们的`getThree()`函数可能是这样的(返回值 3):

```
const getThree = function() {
    return 3;
}
```

# 计算枚举

枚举可以是计算出来的(即计算)，也可以引用其他枚举。例如:

```
enum FirstEnum {
    One,   // Returns "0"
    Two,   // Returns "1"
    Three  // Returns "2"
}enum AnotherEnum {
    One: FirstEnum.One, // returns FirstEnum.One, i.e. "0"
    Two: 1 + 1,         // Calculates and returns "2"
    Three: 1 * 3,       // Calculates and returns "3"
    Star: One           // Refers to AnotherEnum.One, returns "0"
}
```

# 结论

枚举是在 TypeScript 中向代码添加更多语义的一种强大方法。他们让阅读你的代码的人知道你试图完成什么，从而提高你所写的东西的可维护性。通过允许您在整个代码库中引用标准常量，它们也让您的生活变得更加轻松。

我们希望你喜欢这个打字本枚举指南！[要了解更多关于 TypeScript 的信息，请点击这里](https://fjolt.com/category/typescript)。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*