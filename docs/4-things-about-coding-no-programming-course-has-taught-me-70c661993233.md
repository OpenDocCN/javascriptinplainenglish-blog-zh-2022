# “编程课程”没有教给我的 4 件愚蠢的简单事情

> 原文：<https://javascript.plainenglish.io/4-things-about-coding-no-programming-course-has-taught-me-70c661993233?source=collection_archive---------2----------------------->

## 我希望我能早点学会它们。

![](img/879043942a2799ad6203652dc65c3485.png)

Photo by [Tyler Nix](https://unsplash.com/@nixcreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编程课程是任何高效开发人员的支柱。

他们教会了我们编程的基础知识以及如何构建应用程序。

但是编程课程没有涵盖以下内容:

*   如何编写干净的代码
*   如何处理遗留代码
*   如何读懂别人的代码

在这里，我将讨论大多数编程课程没有涵盖的四个方面。

这些将帮助你保持你的代码整洁，并重构他人的代码。

# 1.从现有函数中提取函数

看看下面的 helloUser()函数:

```
function helloUser(){ printHello(); console.log("My first name is: " + fname);  //statement1 console.log("My last name is : " + lname); //statment2}
```

如果`helloUser()`函数的作用是问候用户，那么`helloUser()` 函数中就不需要语句 1 和语句 2。

语句 1 和语句 2 都可以归入一个函数。函数名可以是`introduceMyself()`。

如果你想使用`helloUser()`中的`introduceMyself()`功能，可以调用它。

下面是重写该函数的方法:

```
function helloUser(){ printHello(); introduceMyself();} function introduceMyself() { console.log("My first name is: " + fname);  //statement1 console.log("My last name is : " + lname); //statment2}
```

## 为什么需要从函数中提取函数？

如果一个函数包含大量的代码行，任何程序员都很难搞清楚任何函数的作用。

当任何函数的代码行数较少时，您可以给该函数起一个正确的名称。作为`introduceMyself` 和`helloUser`会更有可读性。

仅仅通过阅读函数名，就可以知道这个函数是做什么的。

将会有更少的代码重复。当您有一个包含特定代码的专用函数时，您可以在多个地方重用它。

代码中出现的错误会更少，因为可以更准确地检查隔离的功能。

# 2.永远不要写代码来娱乐读者

高效的开发人员从不编写额外的代码。

不必要的额外代码不应该出现在您的代码库中。

假设有数百名开发人员在一个组织中工作。他们每个人都决定添加一行额外的代码，只是为了好玩。代码库的大小将增长成千上万行无用的代码。

这些代码库的大小不仅仅增加了几千行。将来，需要对它进行管理，开发人员需要在代码库上花费更多的时间。这将增加代码库的整体复杂性。

有时候，当我们开发人员编写代码时，我们希望以一种方式编写代码，让下一个阅读代码的开发人员感到有趣。

作为高效的开发人员，我们不应该这样做。作为开发人员，我们的目标不是取悦代码受众。

如果你的应用现在不需要一行代码，就不要写那些多余的代码。

# 3.封装变量

移动数据很困难。

如果要移动数据，需要对数据的所有引用进行更改。

## 为什么需要封装变量

如果数据的访问范围很小，那么你可以很容易地处理它。但是随着数据范围的扩大，管理变得越来越困难。

在任何情况下，如果您想要移动频繁访问的数据，您必须首先封装它。这样，您可以轻松地监控对数据所做的任何更改。

通过封装数据，您将能够停止与数据的耦合。

您不需要封装不可变的数据，因为无论如何它都是不可变的。如果需要，您可以轻松地移动不可变数据。

## 一个例子

请看下面的代码:

```
let person = { firstName: "Rock", lastName: "Doe", age: 48, eyeColour: "brown"};
```

假设你想知道这个人眼睛的颜色。

您将编写以下代码:

```
let str = person.eyeColour;
```

如果您愿意，也可以更改分配的值。

你要这样做:

```
let rep = person;rep = { firstName : "Tom", lastName : "Johnson", age : 68, eyeColour: "red"};
```

## 概述

要进行封装，您需要编写如下代码:

```
let person = { firstName: "Rock", lastName: "Doe",    age: 48, eyeColour: "brown"};function getPerson() { return person;}function setPerson(arg) { person = arg;}
```

一旦以这种方式包装了函数，就可以使用对`person`的引用。

你可以写:

```
let encap = getPerson();console.log(encap.firstName);//result: Rock
```

如果想给对象 person 赋予新的东西，可以使用`setPerson`函数。

```
setPerson({ firstName : "Tom", lastName : "Johnson", age : 68, eyeColour: "red"});console.log(person.firstName);//result: Tom
```

# 4.写代码时不要写奇怪的名字

平庸的程序员有写异国名字的习惯。

异国情调的名字是指提请非必要的注意自己的名字。

这类名称的一个例子是:

```
function killStyle(){ //do whatever you what}
```

上面的函数名`killStyle`会引人注意。

每次任何一个程序员看你的代码，都会好奇。他们将深入研究 killStyle 函数。他们会弄清楚那个`killStyle`功能的作用是什么。

如果`killStyle`函数的作用是移除一个特定的样式，如果你把它叫做`removeStyle`而不是 killStyle 会更好。

一个程序员读你的代码时，如果名字很奇怪，他要么会觉得有趣，要么会觉得被骗了。一旦他们觉得被欺骗了，他们将不再信任你和你的代码。

如果你坚持使用有意义的无聊的旧名字，而不是像`deletify`、`unzip`或`disassemble.`这样奇特的名字，那是最好的

如果你把上面的函数写成这样就更好了:

```
function removeStyle(){ //do whatever you like}
```

# 摘要

1.  尽可能提取函数。
2.  不要写代码来娱乐读者。
3.  需要时封装变量。
4.  写代码的时候不要写外来的名字。

# 你想快速进入程序员的职业生涯吗？

加入一群热爱编程和技术的人。

你可以在这里加入。

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***