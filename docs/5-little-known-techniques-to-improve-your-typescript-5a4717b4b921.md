# 5 个鲜为人知的技术来改善你的打字稿

> 原文：<https://javascript.plainenglish.io/5-little-known-techniques-to-improve-your-typescript-5a4717b4b921?source=collection_archive---------14----------------------->

## 排名第一的 JavaScript 超集中的有用技巧

![](img/3804896591c5289f9f5e60afafebc873.png)

Photo by [Cookie the Pom](https://unsplash.com/@cookiethepom?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

自 2012 年由微软创建以来，TypeScript 一直处于上升趋势。TypeScript 最初是一个低调的项目，旨在提高普通 JavaScript 的可靠性，现在是专业开发人员使用第五多的编程语言。说 TypeScript 无处不在并不夸张。

因为 TypeScript 被如此迅速地采用，许多新开发人员每天都开始他们的 TypeScript 之旅。学习一门新语言需要很多问题和改进的空间。回头看看我前一年的 TypeScript 代码，我经常觉得它应该一起重构。所以，为了开始你的打字旅程，或者扩展你已经无懈可击的知识，这里有 5 个鲜为人知的技巧来提高你的打字水平。

## 1.不可变对象和数组

对象和数组值总是可以被修改，即使被赋值给`const`。

但是如果您希望数组或对象的值保持不变呢？TypeScript 提供了一个简单的解决方案:通过在声明后添加`as const`,值和它们的顺序——在数组的情况下——变得不可变。

## 2.完整的开关盒

`Enums`非常适合开关箱。它们允许您根据一组常量轻松地检查一个值。在下面的例子中,`Fruits`枚举用于查找箱子中的水果，并将其记录到控制台。

但是枚举倾向于扩展。如果我们喜欢另一种水果，比如橘子，会怎么样？我们可以将`ORANGE`添加到枚举中，但是只要开关的情况保持不变，我们就永远不会将‘orange’记录到控制台中。

为了确保一个开关考虑到一个枚举的所有成员，我们可以添加一个详尽的检查。通过将案例中的`default`值键入为`never`，我们暗示该值永远不会达到。因此，当开关不完整，从而可能达到默认值时，将会出现编译错误。

## **3。选择上方的'**`**unknown’**`**'**`**any’**`

打字稿就像衣服上的“一刀切”:适用于任何情况，但不合身，也不讨人喜欢。`any`的问题在于它不是类型安全的，这意味着可能会出现类型错误。

例如，假设我们有一个类型为`any`的变量`a`，它包含一个数字。由于没有类型安全，我们可以将这个数字赋给一个字符串类型的变量，或者称它为函数，这显然会引起问题。

`unknown`是`any`的类型安全对应。这意味着您可以将任何值赋给 unknown，但是*不能将 unknown 赋给任何值。因此，虽然使用`any`完全违背了类型脚本的目的，但是`unknown`允许在不牺牲类型安全性的情况下处理不明确的类型。*

## 4.动态验证对象键

使用 JavaScript 意味着使用对象。事实上，这意味着处理大量的对象。因此，JS 函数经常接受对象的键作为参数，以动态地从不同类型的对象中获取值。

但是如何保证给定的密钥存在呢？假设您试图使用键`createdAt`获得一个`Date`值，但是这个键被命名为`created`。这类错误会导致令人讨厌的错误和意想不到的行为。

通过利用`generic`类型和`keyof`属性的能力，您可以确保所提供的键名存在。在下面的例子中，我们将第二个参数`dateKey`限制为所提供类型的有效键，消除了不存在键的风险。

[https://gist.github.com/pvaneveld/b9bac53e441411a2242273224a27b4c0](https://gist.github.com/pvaneveld/b9bac53e441411a2242273224a27b4c0)

## **5。使用记录灵活打字**

有时，键-值对的确切类型事先并不知道。由于缺乏信息，这使得接口的创建变得复杂。在这些情况下，TypeScript 的`Record`就派上了用场。

`Record`允许您通过提供允许键和值类型来定义类型。因此，例如，`Record<string, number>`对应于具有字符串类型键和数字类型值的对象。

我们完了。我希望你在这个过程中学到了一些东西。喜欢这篇文章吗？那么我相信你也会喜欢在我下面的文章中找到一些有用的东西。

[](/7-little-known-techniques-to-improve-your-javascript-20a9e870a5fe) [## 提高 JavaScript 的 7 个鲜为人知的技巧

### 世界上最著名的编码语言的隐藏宝石

javascript.plainenglish.io](/7-little-known-techniques-to-improve-your-javascript-20a9e870a5fe) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*