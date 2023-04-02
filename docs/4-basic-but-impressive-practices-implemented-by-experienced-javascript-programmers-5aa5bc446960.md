# 由有经验的 JavaScript 程序员实现的 4 个基本但令人印象深刻的实践

> 原文：<https://javascript.plainenglish.io/4-basic-but-impressive-practices-implemented-by-experienced-javascript-programmers-5aa5bc446960?source=collection_archive---------3----------------------->

## 新手也应该开始遵循这些做法。

![](img/7844b10a1012bdef8be56a5d85ed352c.png)

Photo by armağan başaran from [Pexels](https://www.pexels.com/photo/a-bearded-man-with-cut-out-paper-flowers-on-eyeglasses-9902630/)

使用 JavaScript 编写程序很有趣。有经验的开发人员遵循的某些基本协议令人印象深刻。在这里，我提到了其中的四件事。

# 1.不使用匈牙利符号

匈牙利符号是一种命名约定。

在这种表示法中，每个标识符有两个部分。第一个是类型，第二个是限定符。

*   类型:标识符的任何第一个字符都表明它是哪种类型的对象实例。为此，类型名的一部分被用作标识符的前缀。
*   限定符:名称的剩余部分表明编写变量名的目的。

## 匈牙利符号示例

*   程序员更喜欢在`butPressMe`标识符中输入`butPressM.`，而不是仅仅输入`pressMe`，`but`是按钮类型的前缀，PressMe 是告诉你其存在目的的限定符。
*   比起写`id`，程序员更喜欢写`nId`或者`numberId.`

匈牙利符号帮助程序员在编写变量名时保持一致性。

遵循匈牙利符号的名称为代码的读者提供了更好的阅读体验。

## 匈牙利符号有什么不令人印象深刻的地方

JavaScript 不是静态类型语言。

JavaScript 是一种动态类型语言，这意味着存储在任何变量中的值的类型都可以在运行时改变。

对于静态类型语言来说，这是不正确的。任何静态类型语言都会给出关于使用任何其他类型的编译时警告。这就是为什么，我们作为 JavaScript 开发人员，需要更加小心。

以下是在编写 JavaScript 代码时使用匈牙利符号的更多缺点:

1.  如果一些糟糕的代码在运行时更改了与变量相关联的类型，那么这个名称会让开发人员感到困惑。使用匈牙利符号书写名字的目的并没有实现(如果一个函数改变了字符串中的 nId，它就违背了整个目的)。
2.  仅仅知道变量的类型，开发人员不会理解它存在的目的。如果不使用类型，我们可以编写一个更有意义的无类型变量名称。
3.  当使用匈牙利符号时，代码库变得僵化。如果你想做一些改变，重构上面的代码就变得困难了。

当 JS 开发人员使用匈牙利符号编写变量名时，事情变得平淡无奇(例外:引用 DOM 元素的变量)。

# 2.将原语视为不可变的

作为一名 JavaScript 开发人员，你必须记住所有的原始值都是不可变的。

如果你是第一次阅读这篇文章，是的，这看起来是一个非常基础的观点，但是当你写代码的时候，你必须确保你没有把原语当作可变的。

只有非原始值是可变的。非原始值包括函数和对象。

原始值包括数字、字符串和布尔值。

## 一个例子说明非原语是可变的

以下是分配给变量`subjectList`的主题列表。

```
let subjectList = ['Math' , 'History' , 'Chemistry' , 'Physics']
```

如果您想对主题列表进行任何更改，您可以。如果要用‘生物学’代替‘历史’这个词。

您将编写以下代码:

```
let subjectList = ['Math' , 'History' , 'Chemistry' , 'Physics']subjectList[1] = 'Biology'console.log(subjectList)
```

上述代码的输出将是:

```
['Math' , 'Biology' , 'Chemistry' , 'Physics']
```

## 原始价值的一个例子

原始值是不可变的。

```
let subject = 'Sathematics'
```

上面的`subject`变量有一个 Sathematics 值。

现在假设我们想改变`subject`变量的第一个字母。

让我们编写代码来实现这一点:

```
let subject = 'Sathematics'subject[0] = 'M'console.log(subject)
```

输出将是:

```
Sathematics
```

哦！我们无法更改与主题变量相关联的值。

## 大多数 JavaScript 开发人员在这一点上感到困惑

再取上面的主题列表数组。

```
let subjectList = ['Math' , 'History' , 'Chemistry' , 'Physics']
```

我们希望打印 subjectList 数组中第二个可用的单词。

```
let subjectList = ['Math' , 'History' , 'Chemistry' , 'Physics']console.log(subjectList[1])
```

输出将是:

```
History
```

现在让我们拿一个字符串，试着打印该字符串的第二个字母。

```
let subject = 'MATHEMATICS'console.log(subject[1])
```

上述代码的输出将是:

```
A
```

subjectList[1]和 subject[1]命令都工作得很好，我们可以在那个位置打印可用的内容。

但是正如我们前面看到的，我们不能改变原始的`subject`变量，相反，我们改变了名为`subjectList`的非原始数组。

这意味着原语值在 JavaScript 中是只读的，非原语值是读写的。

## 原始值不能变异，但是变量可以重新分配给新的原始值

许多 JavaScript 开发人员会认为我们仍然可以改变与原语相关的值。

他们会说我们可以做到:

```
let subject = 'Sathematics'subject = 'Mathematics'console.log(subject)
```

这将是输出:

```
Mathematics
```

使用上面的代码，我们将能够改变与`subject`变量相关的值，但是我们没有改变这个值。

我们没有改变这个值，而是给`subject`变量重新分配一个新的原始值。

对上述讨论的一行总结是，原始值不能被改变，但是变量可以被重新分配给一个新的原始值。

# 3.通用命名模式的使用

通用命名模式有助于保持我们代码库的一致性。

当您应用通用命名模式时，任何代码的读者都会清楚地了解您的代码。这有助于我们避免任何形式的困惑。

如果你创建了一个具有复杂名字的类，在这个类中，我们定义了许多函数来帮助不同数字的加、减、乘。

要删除数字，如果我们开始使用这样的命名模式:

```
class Complex{ removeNumber() {}
    deleteNumberIfDuplicate() {}
    eradicateNumberIfExtra() {}}
```

…在审查代码时，任何人都会开始感到困惑。在复杂类中，为了做几乎相似的事情，使用了三种不同的变体。

三种不同的变体包括`removing`、`deleting`和`eradicating`。

上面三个名字指的都是一样的东西。如果能使用这样相同的命名模式就更好了:

```
class Complex(){

    removeNumber() {}
    removeNumberIfDuplicate() {}
    removeNumberIfExtra() {}}
```

有了上面的命名风格，事情就变得好理解了。

如果有人试图使用上述抽象，他们不必记得删除、移除和根除。这将帮助他们维护整个代码库的一致性。

# 4.他们不允许一个单元与一个陌生的单元直接交互

一个单元可以代表任何函数、模块或类。

这里的交互表示调用另一个单元的代码。

## 现实生活中的例子

我们想象一个场景，一个人把自己的车卖给另一个人。

买车的人有一个放钱的钱包。

该类将如下所示:

```
class carBuyer(){ constructor(){ this.purse = new carBuyerPurse();
    }
}
```

carBuyerPurse 类如下所示:

```
class carBuyerPurse { constructor(){

        this.money = 0
    } add(received) { this.money += received
    } debit(give){

        this.money -= give

    }
```

现在假设一个程序员 Bob 写了下面的代码来成功销售。

```
class carSeller1 { sale(carNo, CarBuyer){ const cost = carNo.cost() carBuyer.purse.debit(cost) // Do whatever you want }}
```

Bob 写完上面的函数，觉得既然上面的代码管用，那就写吧。

不，但是鲍勃忽略了一件重要的事情。

如果我们试着分析上面的`carSeller1` a 类，你会注意到汽车销售商拿走汽车购买者的钱包，然后打开那个钱包，自己从钱包里拿出汽车的成本。

在上面的场景中，汽车销售员在没有征得购车者同意的情况下，拿走了他的钱包，并从钱包中取出了现金。在现实生活中，一个汽车销售员永远不可能做到这一点。

如果购车者想用信用卡而不是现金付款，那该怎么办？购车者的钱包里可能有也可能没有足够的现金。

`carSeller1`类犯了两个错误:

*   直接和陌生的班级互动。
*   对陌生人阶层做出假设。

## 做事的正确方式

carSeller 函数应该如下所示:

```
class carSeller2 { sales(carNo, carBuyer) { const cost = carNo.cost() carBuyer.requestCost(cost) }} 
```

你可能认为我们增加了程序的复杂性。

`carSeller1`类很短，但它在做复杂的东西，从长远来看，干净的抽象会有用得多。

现在任何程序员都可以使用`requestCost`函数设计一个简洁的抽象。

# 摘要

1.  不要事事都遵循匈牙利符号。
2.  不要把原语视为可变的。
3.  使用常见的命名模式。
4.  直接和陌生人互动不好。

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

你可以在这里加入。

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*