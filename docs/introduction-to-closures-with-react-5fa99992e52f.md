# React 闭包简介

> 原文：<https://javascript.plainenglish.io/introduction-to-closures-with-react-5fa99992e52f?source=collection_archive---------5----------------------->

![](img/aaef5cb1fccdabfbd164eb5377c8bfe8.png)

很可能，您已经使用闭包很长时间了，甚至没有意识到这一点。

*一个* ***闭包*** *是用对其周围状态的引用捆绑在一起(括起来)的函数的组合(词法环境***)。**

*如果您在理解什么是闭包或者如何使用闭包方面有困难，本文将对这两者进行介绍。我将展示一个非常简单的 React 组件中闭包的例子。我的目标是提供一个简单的介绍，介绍闭包是什么，它们是如何工作的，以及你最有可能在哪里使用它们。*

*简单的闭包示例:*

*在上面的例子中，我们使用一个函数为列表中的每篇文章创建一个 URL。该函数使用传递给它的参数，以及在外部函数中声明的 uid 变量。*

*在我参与的 React 项目中，我一直使用这种模式。在讨论闭包时，通常会引用全局状态变量。*

*我们声明的每个函数都有可能成为闭包。当函数引用其直接作用域之外的变量时，就会出现闭包。它们通过在创建函数时将对外部变量的引用与函数体的其余部分捆绑在一起来实现这一点。当谈到闭包时，函数之外的区域被称为词法环境。*

*记住这一点，getPostUrl 函数就是一个闭包的例子，因为它引用了我们的词法环境中的 uid 变量。*

*您引用的外部变量不必属于一个全局状态对象来进行闭包。*

*如果您要引用 myHelperFunc 函数或 Intl API，您也将创建一个闭包。*

*在学习复杂的 javascript 模式(如闭包)时，我经常欣赏简单的起点。从那里开始，我发现进入更复杂的特性要容易得多。我希望这有助于任何努力开始的人。*

*这里有一些很好的资源，可以让你更深入地理解闭包:*

 *[## JavaScript 闭包及其用法初学者指南

### 摘要:在本教程中，您将了解 JavaScript 闭包，以及如何在代码中使用闭包…

www.javascripttutorial.net](https://www.javascripttutorial.net/javascript-closure/)* *[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) [## 闭包- JavaScript | MDN

### 闭包是捆绑在一起(封闭的)的函数与对其周围状态的引用的组合

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) 

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*****[***免费每周简讯***](http://newsletter.plainenglish.io/) ***。*** *在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***中获得独家写作机会和建议。******