# 你不应该再写普通的 JavaScript 代码了

> 原文：<https://javascript.plainenglish.io/you-should-never-write-plain-javascript-code-again-719c5b8fbcd3?source=collection_archive---------2----------------------->

也许标题看起来有点像 click 诱饵，但是我相信在本文之后，每个人都不应该编写动态类型的 JavaScript 代码！

![](img/07e0481ee3a82a9d9f9d35e6c66dda92.png)

Photo by [Gabriel](https://unsplash.com/@natural?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 为什么不是普通的 JavaScript？！

JavaScript 的一个警告或好处是，作为一种动态类型的语言，它意味着您不必将严格类型的变量或 void 返回值放在前面。如果你只是一个人，在你的 20 行小 javascript 代码上工作，那么你可以忽略静态类型，但是请不要再编写没有静态类型的代码了！

我们可以忽略过去几年不使用 TypeScript 的原因，因为缺少对它的库和框架支持以及覆盖，但是现在希望覆盖范围足够了。

# 为什么是静态类型的？

我认为最大的原因是代码的**可预测性**和**可读性**的天赋，静态类型化之前的代码可以是任何东西！绝对可以。假设您有一个名为“ **user”的变量，**然后想想这个变量可能是什么，它可以是字符串、数字、对象、Promise 或任何其他东西！

```
let user;
// string?
// number?
// object?
// function?
```

为什么这很重要？当你在编码的时候，知道你的代码会被其他人使用和阅读，甚至在 1 年内被你自己使用和阅读，那么你应该站在那个人的立场，想想他们是如何看待代码的。他们会怎么做？他们能理解目的吗？如果这个问题没有意义，那么你可以跳过这篇文章。

现在让我们看看下面代码的静态类型版本；

```
let user: string;
// Yeah! it will be string.
```

# 有哪些选择？

我们没有太多静态键入 JavaScript 的选项，实际上，最常用的是 [**TypeScript**](https://www.typescriptlang.org/) **。**

我们有其他的选择，比如[流](https://flow.org/)或者一些 IDE 扩展，但是他们甚至不是 TypeScript 的竞争对手。

# 以打字打的文件

TypeScript 是一种强(静态)类型语言的 JavaScript 超集，这意味着您的代码具有 TypeScript 的语法，但最终您会得到一个用于输出的 JavaScript 代码。

乍一看，语法可能有点疯狂，对于一个总是用动态类型语言编码的人来说，这是完全正常的，所以不要害怕: )

让我们看看这份礼物的一些例子！

```
let user: string;

function phone_verifier(phone: number): bool {
  return true;
};
```

太棒了！你知道你写的是什么，目的是什么，别人也会这么做。

感谢您阅读本文，如果您介意看到更多类似的内容，您可以快速查看[我的中页](http://medium.com/@sinafarhadi)。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***