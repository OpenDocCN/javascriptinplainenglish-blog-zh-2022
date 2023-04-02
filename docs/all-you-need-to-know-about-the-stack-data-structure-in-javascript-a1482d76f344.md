# 关于 JavaScript 中的堆栈数据结构，您只需要知道

> 原文：<https://javascript.plainenglish.io/all-you-need-to-know-about-the-stack-data-structure-in-javascript-a1482d76f344?source=collection_archive---------10----------------------->

## 堆栈如何工作以及如何在自己的程序中使用它们。

![](img/4532e92d18a1f638808314bbd2f2e85b.png)

Photo by [Debby Hudson](https://unsplash.com/@hudsoncrafted?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

堆栈是一种数据结构，它允许你以后进先出的方式存储和访问数据。这意味着堆栈顶部的项是第一个被移除的项。堆栈通常在编程中用于处理输入和输出，或者跟踪正在处理的项目。在这篇博文中，我们将讨论堆栈是如何工作的，以及如何在自己的程序中使用它们！

## 后进先出原则

正如我们之前提到的，堆栈使用后进先出原则。这意味着最近添加到堆栈中的项将是第一个被移除的项。为了形象化这一点，想象一堆书。如果您将一本新书添加到堆栈的顶部，当您开始从堆栈中取出书籍时，它将是第一个被移除的书。

你可以把栈想象成一个有两端的容器:顶部和底部。项目被添加到堆栈的顶部，也从顶部移除。这允许您访问堆栈中最近的项目，而不必先移除所有其他项目。

## JavaScript 中的堆栈实现

现在我们已经知道了堆栈的一般工作方式，让我们看看它们是如何在 JavaScript 中实现的。在 JavaScript 中，没有内置的堆栈数据结构。然而，我们可以通过使用数组来实现堆栈的功能。

![](img/ba6151acd051c1eb2e54ecaafd41a0a2.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 添加和删除项目

将一个项目添加到堆栈中称为推送。要将一个项目添加到堆栈中，只需将它放在堆栈的顶部。

```
let stack = [];stack.push(val);
```

从堆栈中移除一个项目称为 pop。要从堆栈中删除一个项目，您需要从堆栈中取出顶部的项目并将其放在一边。它下面的项目成为新的顶部项目。

```
let stack = [12, 13];let val = stack.pop();return val; // 13
```

## 检查堆栈是否为空

知道堆栈是否为空是很有用的。为此，您可以使用。长度属性:

```
let stack = [];if (stack.length === 0) { console.log(“Stack is empty”);} 
else { console.log(“Stack is not empty”);}
```

## 获取堆栈的顶部元素

如果你想在不移除栈顶元素的情况下获取它，我们可以实现一个 peek()方法。

```
function peek(stack) { if (stack.length === 0) return null; return stack[stack.length — 1];}let stack = [12, 13];console.log(peek(stack)); // 13
```

## 结论

堆栈是一种强大的数据结构，可以以多种不同的方式使用。通过理解它们如何工作以及如何用 JavaScript 实现它们，您可以在自己的程序中使用它们！祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***