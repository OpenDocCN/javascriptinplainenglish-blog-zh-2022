# 一个没有经验的程序员犯的 4 个奇怪的错误，很少有人提及

> 原文：<https://javascript.plainenglish.io/4-strange-mistakes-of-an-inexperienced-programmer-hardly-anyone-mentions-a247345af942?source=collection_archive---------7----------------------->

## 不犯这些错误是一种超能力

![](img/cdb1db53db064acdbb635f6c1a91e1b0.png)

Photo by [Andrea Piacquadio](https://www.pexels.com/@olly?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-in-white-crew-neck-t-shirt-sticking-his-tongue-out-3799786/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

这个故事背后是 Medium 的会员付费墙，这意味着作者通过合作伙伴计划获得收入。喜欢在媒体上阅读？ [*购买会员资格*](https://sanjay-priyadarshi.medium.com/membership) *获取全部权限。*

程序员通过犯错来学习。

但是当你开始你的程序员生涯时。你没有多少经验可以从错误中吸取教训。

当你在写代码的过程中，也很难发现这些错误。

在和一百多个开发者互动并指导他们之后。我发现了这些没有经验的程序员经常犯的错误。

作为一个程序员，你应该避免这些错误。

# 1.有一种“以后再解决”的心态

下一次迭代将带来一种新的头痛。

大多数没有经验的程序员为了速度而优化。当他们必须在“做对”和“做快”之间做出选择时

很多时候他们选择“速战速决”他们认为他们以后会回来改正他们所有的错误。但是当他们进行下一次迭代时，他们会被新的问题包围。

在下一次迭代中，他们发现关注新问题比解决老问题更重要。这个东西叫技术债。

技术债务是程序员生产力的敌人。

大多数程序员受益于短期技术债务。因为他们使用快捷方式并保持低质量的代码。他们很快完成了项目。

技术债务的长期后果可能是灾难性的。

当您在代码中使用快捷方式时，添加新功能会变得更加困难。用快捷方式重构代码很难。有了快捷方式，管理大型代码库变得很困难。

你把技术债务拖得越久，它会引起越多的问题。

作为一名程序员，会有你不得不承担一些技术债务的情况。在这种情况下，你需要尽快回去还清债务。

如果你不尽快解决技术债务，你就是在召唤怪物。

# 2.没有应用函数式编程原则

函数式编程极大地提高了代码质量。

大多数程序员要么不懂函数式编程(fp)，要么即使懂了也不用。

当你只使用函数编写程序时，它被称为 fp。在 fp 中，表达和定义你的逻辑的主要方式只有通过函数才有可能。

函数式编程有助于程序员轻松调试代码，也有助于保持并发安全。

## 首先理解不纯函数，然后我们将继续函数式编程

假设您编写了以下函数:

```
let abc = 0function addNumber(num){
    abc = abc + num;
    return abc;
}
```

当多次调用上述函数时，不会给出相同的输出。

让我们看看这个例子:

```
addNumber(5);
console.log(addNumber(5));
```

在上面的代码中，您已经调用了 addNumber()两次。以上代码产生的结果:

```
// This is the output
10
```

如果你再调用一次 addNumber 函数。它将产生不同的输出:

```
addNumber(5);
addNumber(5);
console.log(addNumber(5));// This is the output
15
```

上面的 addNumber()就是一个不纯函数的例子。

上面的函数改变了其作用域之外的变量。addNumber()产生的结果每次都会改变，即使输入相同。

## 纯函数是函数式编程的一部分。

在函数式编程的情况下，定义的函数就像数学函数。

数学函数可以进行计算。同样，fp 函数可以做计算。这些函数称为纯函数。

这就是如何编写一个纯函数:

```
function addPure(num1, num2){ return num1 + num2;
}
```

无论你调用多少次上面的函数，上面的函数都会给出相同的结果。

你可以调用 pure 函数:

*   一次。
*   两次。
*   三次。

没关系。输出不会改变。

```
addPure(0,5);
addPure(0,5);
console.log(addPure(0,5));// This is the output
5
```

上面的纯函数 addPure()不会改变其作用域之外的变量的值。

此外，每次执行函数时，输出不会改变。

纯函数可以基于输入参数执行计算或计算任何值。你也可以称纯函数为确定性函数。

```
Math.random and Date.now are not example of deterministic functions as they produce a different output every time they are called.
```

## 函数式编程会让你看起来像个天才

*   纯函数确保外部程序的状态不会改变。没有任何局部静态变量的突变。
*   测试纯函数非常容易，因为输出只取决于输入。纯函数不依赖于输入以外的任何状态。
*   因为每个函数都将一个输入映射到一个输出，所以调试代码将会很容易。即使使用打印语句，您也可以检查错误。

# 3.他们没有维护期望的编码标准

每个新项目都以新的代码解析开始。

所有参与该项目的程序员都会收到文档。本文档包含所有代码解析。参与该项目的程序员同意遵循所有这些决议。

起初，没有经验的程序员工作缓慢，认为他们有足够的时间来完成他的工作。他们首先遵循所有期望的编码标准。

但是当最后期限开始临近，压力开始增大时，他们就不关心格式良好的代码了。他们所想的只是他们必须添加多少功能。

让我们看一个例子:

假设程序员被要求添加四个空格来缩进他们的代码。基本代码中的任何函数看起来都像这样:

```
function addNumber(num1, num2){
    return num1 + num2;
}
```

当压力开始增大时，他们可以开始只使用两个空格来缩进代码。上面的代码看起来会像这样:

```
function addNumber(num1, num2){
  return num1 + num2;
}
```

你可以认为这是一件小事。

但是当这种事情随着时间的推移而重复时，整个代码库开始看起来像一团乱麻。没有一个未来的程序员会喜欢使用混乱的代码库。

对于这些类型的程序员来说，满足最后期限是最重要的任务。

## 可以采取几个步骤来解决这个问题:

1.  所有编码标准必须自动化。
2.  代码的格式化应该是构建过程的一部分。这将确保所有开发人员自动运行它。
3.  不是所有的事情都可以自动化。为了解决这个问题，一个组织必须编写一些额外的指南，并将它们分发给开发人员。
4.  应该使用能够很容易地检测出不需要的模式的代码分析工具。

# 4.不考虑现有的代码库

激动人心的代码库有一定的优势。

没有经验的程序员认为，他们可以更好地重构代码库，而无需考虑现有的代码库。但现实恰恰相反。

当他们开始重组代码库而不考虑现有的代码库时，他们最终会造成混乱。他们不关心现有代码库的优缺点。

它们没有考虑一些现有的测试用例。他们不试图理解为什么一个特定的测试用例会出现在那里。他们只关心自己看起来有多聪明。

为了重构代码库，他们必须分析现有系统的优缺点。这将有助于他们理解先前版本的代码中的一些关键错误。

这样，他们将确保现有代码库中的错误和弱点不会在他们重构代码时困扰他们。

为现有代码库编写的测试用例可以给你独特的见解。

不要忽视现有的代码库。它已经过审查和测试。寻找优势，尽可能利用它们。

# 摘要

1.  “以后再解决”的心态是生产力杀手。
2.  不使用函数式编程原则是不好的。
3.  没有遵循适当的编码标准。
4.  现有的代码库和测试用例可以节省您的时间。

[点击这里](https://codertoentrepreneurs.substack.com/)加入一个由热爱编程和技术的人组成的社区。喜欢在媒体上阅读？[购买会员资格](https://sanjay-priyadarshi.medium.com/membership)获得全部权限。

[](https://sanjay-priyadarshi.medium.com/membership) [## 通过我的推荐链接加入 Medium-Sanjay Priyadarshi

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

sanjay-priyadarshi.medium.com](https://sanjay-priyadarshi.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*