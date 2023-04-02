# JavaScript 中 bind()方法的介绍

> 原文：<https://javascript.plainenglish.io/an-introduction-to-the-bind-method-in-javascript-77cd820af40d?source=collection_archive---------6----------------------->

## 用例子理解 bind()方法。

![](img/aebdcb96fb6d49754bd3b2cf30e7d24a.png)

Photo by [Dan Bucko](https://unsplash.com/@danbuckophotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在关于函数借用的 JavaScript 系列的第 3 部分中，我们将看看 bind()函数。在此之前，为了有一个更好的理解，请通过该系列的其他 2 部分。

*   [呼叫](/call-in-javascript-3048c300bb29)
*   [敷](/apply-in-javascript-1848c41ae5f4)

现在，一旦您对调用和应用有了更好的理解，让我们看看绑定是如何工作的。

Bind 的工作方式与 call 非常相似，唯一的区别是 bind 是延迟加载的，也就是说，它不会被立即调用。

让我们用例子来更好地理解它。

```
// Block 1const nameDetail = {getName: function () {return this.name;},}; // Block 2const myName = {name: 'Avinash',}; // Block 3let readNameFunc = nameDetail.getName; // Block 4let readName = readNameFunc.bind(myName);// Block 5console.log(readName());   // Avinash
```

现在，上面的代码片段中发生了什么？

让我们一步步了解:

*   **模块 1** :我们已经定义了一个对象，它封装了一个服务于通用目的的函数，即 getName
*   **Block 2** :我们已经定义了一个要打印其值的对象。(可以有多个这样的对象，然后重用块 1 中定义的同一个函数)
*   这是魔法开始发生的地方。我们已经将函数定义赋给了 readNameFunc 变量。
*   **Block 4** :在这个部分中，readNameFunc 函数被绑定到一个对象上，这个对象被 bind 函数中传递的第一个参数所引用。
    ***快速复习—就像调用和应用一样，绑定也是函数原型中存在的一个函数。***

如上所述，bind()在这个阶段没有被调用，相反，在这个阶段，只有关联的函数与对象一起使用。

*   **块 5** :这里我们只是简单地调用块 4 中的赋值函数，我们观察到函数内部的这个值与绑定对象的值相同。

这就是 bind()函数的工作原理。

你可能会问的一个问题是，在块 4 中，我们已经用函数附加了一个对象，如果我们不把它绑定到一个特定的对象上呢？
答案是→在这种情况下，函数将指向窗口对象，如果找到同名变量，将返回 else，将返回 undefined。

这一点在下面的片段中会更加清楚:

```
this.name = 'Abhishek';const nameDetail = {getName: function () {return this.name;},};let readNameFunc = nameDetail.getName;let readName = readNameFunc.bind();console.log(readName());   // Abhishek
```

因此，与前面的代码片段不同，没有提供任何对象来与 readNameFunc 绑定。在这种情况下，readName 将指向全局窗口对象，并相应地提供输出。

现在，还有一件事你应该知道，这里类似于调用，我们可以传递额外的参数给绑定函数，从第二个参数开始。

为了更清楚起见，让我们看看下面的片段:

```
const nameDetail = {getName: function (stack) {return `${this.name} is a ${stack} developer`;},};const myName = {name: 'Avinash',};let readNameFunc = nameDetail.getName;let readName = readNameFunc.bind(myName, 'Javascript');console.log(readName()); // Avinash is a Javascript developer
```

这里，我们在将函数绑定到对象时传递了额外的参数，这些参数可以在调用时使用。

这就是 bind 的工作原理。

我希望，通过本系列，您能够更好地理解 call()、apply()和 bind()。

总结一下这三个例子，你可以参考下面的截图来快速对比这三个例子。

![](img/db27d63b35053f71408f0455a641ee6d.png)

Summary

希望这个系列对你们所有人都有帮助，并且你们在经历这些的时候取得了一些进步。如果您有任何反馈或建议，请告诉我。

你可以从[这里](https://medium.com/@avinash.dev21987)阅读我的其他文章，此外你还可以订阅我的时事通讯以获得我发表的最新话题。

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*