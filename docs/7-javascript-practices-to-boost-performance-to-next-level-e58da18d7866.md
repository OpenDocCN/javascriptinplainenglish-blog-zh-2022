# 将性能提升到下一个 Level⚡的 7 个 JavaScript 实践

> 原文：<https://javascript.plainenglish.io/7-javascript-practices-to-boost-performance-to-next-level-e58da18d7866?source=collection_archive---------10----------------------->

## 如果你想提高你的代码的速度，那该怎么办呢？

![](img/03cfdbb15b83b7e9daed0f3e13b1d665.png)

如今，JavaScript 是网络上以及本地移动和桌面应用中最常用的编程语言之一。这也是开发人员最常学习的技能之一，即使您不打算在未来的项目中直接或间接使用它。那么为什么这么多人选择这种语言呢？是什么让它如此特别，受到这么多人的喜爱？为了回答这些问题，我们需要回顾一下它成为当今世界上使用最多的编程语言的主要原因，以及在 2018 年使用 JavaScript 时，哪些做法被认为是好的(哪些是坏的)。

# 建立一个节省打字时间的环境

如今 JavaScript 性能成为问题的一个关键原因是隐式类型转换。当在单个表达式中，一个操作数的数据类型可以转换为匹配(*或强制转换为*)另一个操作数的数据类型时，JavaScript 中会发生隐式类型转换。

这可能不清楚，所以让我们看一些例子。当您在 JavaScript 中添加 **2** 和 **3** 时，它会在执行任何计算之前隐式地将两个操作数转换为数字:( ***+ 2 3*** )计算结果为 **5** ，并且(***2+3****)*计算结果也为 **5** 。

# 对常见任务使用简写映射

简写映射是在 JavaScript 中执行常见任务的一种快捷方式。最好的例子可能是**数组析构**，它允许你写这样的东西

```
[key, value] = myArray instead of Object.assign(, myArray)
```

它节省了时间和空间，但更重要的是，它通过减少函数调用开销提高了性能(*您多久执行一次* [***)。在空对象上赋值()***](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) *？*)。如果这看起来令人困惑，不要担心，一旦你习惯了它，它并不那么难，如果你想更深入地了解速记映射，那里有一些很好的资源。

# 不断清理你的代码

混乱的代码库是导致灾难的原因。即使你的 JavaScript 可以工作，当你有几十万行代码时，它也很容易变得过时或者有问题。

为了提高性能，不断关注你的代码库，清理不必要的元素或实践。像 [**Webpack**](https://webpack.js.org/) 这样的工具可以让你知道什么时候模块没有被使用，这样你就可以放心地把它们从你的项目中移除。关键是对如何和为什么写每一行代码保持一种有组织的心态——然后定期回顾以确保在你的项目中没有什么是未使用的或多余的。

# 使用模块和库，而不是重新发明轮子

JavaScript 最大的优势之一是它的 [**开源**](https://www.codementor.io/@jennifercarnel/top-10-open-source-javascript-libraries-1npwdey1be) **社区**。很多开发工作已经为你完成了，这意味着使用**模块和库**是一个好主意，而不是试图自己重新发明每一个轮子。

但是安装新的软件包时要小心；不是所有的都像其他的一样维护的很好。如果你导入太多的外部依赖，你的代码库将会变得混乱，所以要限制它们！

# 理解 JS 数组和对象

都说 web 开发者要时刻想着性能。这是真的，因为高绩效与仅仅是好有很大的不同。事实是，您可以在 JavaScript 中做许多小事情来显著提高其性能，并且您应该**在继续您的开发工作流程之前仔细考虑它们**。

# 使用带有承诺而不是回调的异步函数

JavaScript 最大的性能提升来自于从回调到承诺的转换。异步函数甚至比承诺的还要快，而且没有损失可读性。如果你有回调，花点时间用 async/await 或 promises 重写它们。

您会惊讶地发现，在不牺牲可读性的情况下，您的代码变得如此简单。(如果你不确定这些术语的意思，可以考虑查看 Mozilla 开发者网络[](https://developer.mozilla.org/es/docs/Web/JavaScript)**页面，了解异步编程模式。)**

# **时刻关注性能**

**首先，要知道 JavaScript 性能很重要。不是每个人都明白这对他们的最终用户和他们自己有多重要。如果你想让你的应用变得更快，从开发过程的第一天开始就考虑性能。**从第 1 天开始运行一个** [**剖析器**](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/)**(*或之前*)和 t **机架代码级度量**，如方法持续时间、分配/引用的对象数量、GC 暂停时间等。****

****在整个开发过程中，使用这些数字作为早期代码**红色警告标志**。无论是通过遥测还是通过手动检查您的配置文件数据(*，我强烈推荐*)，您越能深入了解源代码执行和整体内存使用模式，您就越能从应用程序或网站中获得出色的性能。****

## ****作为特色的****

****[https://webpack.js.org/](https://webpack.js.org/)****

****[https://www . smashingmagazine . com/2012/06/JavaScript-profiling-chrome-developer-tools/](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/)****

****[https://developer . Mozilla . org/es/docs/Web/JavaScript/Reference/Global _ Objects/Object/assign](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)****

****[https://www . code mentor . io/@ Jennifer carnel/top-10-开源-JavaScript-libraries-1 npwdey 1 be](https://www.codementor.io/@jennifercarnel/top-10-open-source-javascript-libraries-1npwdey1be)****

****[https://developer.mozilla.org/es/docs/Web/JavaScript](https://developer.mozilla.org/es/docs/Web/JavaScript)****