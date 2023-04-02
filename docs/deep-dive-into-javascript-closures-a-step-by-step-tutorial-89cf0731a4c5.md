# 深入研究 JavaScript 闭包:分步教程

> 原文：<https://javascript.plainenglish.io/deep-dive-into-javascript-closures-a-step-by-step-tutorial-89cf0731a4c5?source=collection_archive---------7----------------------->

## 从理论和实践的角度理解闭包。

![](img/92865c6b7d35a8c883701feab185650d.png)

Image created by myself

> 你好，如果你想自己体验媒介，请考虑**支持**我和所有其他作家，注册一个 [**会员**](https://medium.com/@anton.franzen/membership) 每月 5 美元，以保持独立写作的活力， [**在这里注册；)**](https://medium.com/@anton.franzen/membership)
> 
> 除了支持他人，Medium 还可以通过写作和在这里找到家的强大、积极参与的社区来支持你。

这个主题可能会很混乱，因为关于它是什么有如此不同的解释，而且它对 JavaScript 开发人员来说也很神秘，因为它一直在使用，但没有多少人知道它到底是如何工作的。

我最近拿起了第二版的`You Dont Know JS Yet`来填补我知识上的一些空白，在那里他谈到了闭包，我认为它非常有意义，尽管我已经知道什么是闭包，我从另一个角度了解了它的内部工作。所以在这篇文章中，我将从我的角度解释闭包是如何工作的以及它们是如何被使用的！

**我们将复习的内容:**

1.  闭包的定义
2.  闭包的简单解释
3.  一个闭包的深层解释

> 你好！你想每周在邮箱里收到 ***独家*** *关于****full stack JavaScript 开发*** *的内容、技巧和窍门吗？点击* ***此处*** *免费访问。*

**1。首先让我们看看** `mdn` **对闭包的定义:**

> *闭包是对其周围状态(词法环境)的引用捆绑在一起(封闭)的函数的组合。换句话说，闭包允许您从内部函数访问外部函数的范围。在 JavaScript 中，闭包是在每次创建函数时创建的。*

好的，我们可以把它看作是另一个函数内部的一个函数，这个函数可以访问外部函数的变量，是的，这没有多大意义，但是如果你看下面的代码，它可能会这样做:

```
function outer() {
const outerVariable = "Hey!"
function inner() {
console.log(outerVariable)
}
inner()
}
outer() // "Hey!"
```

正如我们看到的函数`inner`可以访问变量`outerVariable`

这是因为当我们调用函数`outer`时，函数`outer`创建了一个名为`outerVariable`的局部变量和一个函数`inner`，所以函数`inner`可以访问这个变量。

所有的函数都在创建阶段创建一个`closure`，我们将在后面讨论，但是我们上面的例子并没有真正使用`closure`功能。

只是快速解释一下不同范围的行话会让你感到困惑:

> ***范围:***
> 
> *作用域是当前执行的上下文，作用域在哪里执行？是全局执行吗？那么作用域是全局的，是函数执行吗？那么这个范围就是局部范围。*
> 
> ***局部范围:***
> 
> *局部作用域如果我们在函数内部声明一个变量，那么它就在该函数的局部作用域内。Short:是指我们的代码中可以访问的受限区域。*
> 
> ***全局范围:***
> 
> 全局作用域是指在我们文件的根中声明的变量，意思是不在任何其他作用域内。

我希望这有意义，这只是经典的范围和可访问性的东西。

现在让我们更深入地了解一下确切的闭包是什么，尽管我们刚刚写了一个闭包。

# 2.闭包的简单解释

我是这样看待什么是终结的:

> *闭包是指函数可以访问自己作用域之外的变量，并随着时间的推移记住它们，即使该函数是从另一个作用域执行的。*

我是从上面提到的那本书里得到这个观点的。

让我们弄清楚:闭包在 JavaScript 中无处不在。

例如，这个*是*一个闭包:

```
function closure(args){
return function inner(){
return args
}
}
const x = 10;
const useClosure = closure(x)
useClosure()
```

没有必要做复杂的例子来理解什么是结束，我刚刚做的就是一个结束，就是这样…

但是为了深入理解它，我们需要进入更复杂的例子。

但还是继续说这个简单的例子吧。

函数`inner`正在关闭函数`closure`的执行上下文环境，*我们将在后面详细讨论！*

这就给我们留下了之前说过的定义:

闭包是一个函数，它可以访问其作用域之外的变量，并且可以从另一个作用域调用。

# 3.一个闭包的深层解释

在深入研究之前，我们需要了解 javascript 中的全局执行上下文。

Javascript 有两个全局执行上下文阶段，一个创建阶段和一个执行阶段。因此，当我们运行 javascript 文件时，将执行全局执行上下文，这是第一个阶段，即创建阶段。

> ***创作阶段:***
> 
> *创建了* ***窗口*** ***对象*******这个*** *关键字就是指窗口对象。**
> 
> **赋值* ***未定义*** *给所有* ***变量****&****函数*** *用****var****关键字声明，这叫做***。***
> 
> ***为* ***全局作用域*** *中的所有* ***函数声明*** *创建内存。***
> 
> *****执行阶段:*****
> 
> ***从上到下逐行执行 javascript 文件。***
> 
> ***将* ***值*** *赋值给我们的* ***变量*******函数表达式*** *等。****

**现在有 1 个最后的执行阶段，称为**函数执行上下文**。**

> *****功能执行上下文:*****
> 
> ***创建一个* ***参数*******对象*** *。****
> 
> ***创建一个* ***对象*** *称为* ***这个*****
> 
> ***赋值* ***未定义*** *给所有* ***变量****&****函数*** *用****var****关键字声明，这就叫***
> 
> ***为* ***局部范围内的所有* ***函数声明*** *创建内存。*****

**函数执行上下文仅在函数被调用时创建，仅在函数被调用时创建。**

**当函数被调用时，它被推到**调用栈**并创建变量，但是一旦函数**返回**，它就被**从**调用栈**中弹出**，并且变量不再存在，这就是为什么我们不能访问它所在的局部范围之外的变量。**

**现在，当我们解决了这个问题，让我们再次回到闭包。**

**每个函数**在**创建阶段**都会创建一个闭包**，但是要真正使用**闭包**的**特性**，我们能做的就是**在函数中返回**一个**内部函数**，并且**内部函数**会在**父函数执行上下文环境**上创建一个**闭包作用域**。这样我们通过**作用域链**让**访问**到**参数**和**变量**。**

# **关键点:**

```
**function first(args){
const foo = args
return function inner(){
return foo
}
}
const a = first(10)
a() // will return 10**
```

**当我们**调用**上面的**函数**时，会发生这种情况:**

****函数创建阶段:**创建一个**自变量** **对象**，**该对象**，将**变量**赋值给**变量**未定义的**，将**函数声明**添加到**内存中。******

****函数执行阶段:**它被推送到**调用栈**，将**值**赋给**变量**、**函数表达式、**等，从上到下运行函数中的代码，一旦到达底部，它将返回，**将**弹出**调用栈**并将函数中的所有内容**但是:****

**内部函数是**在**父函数执行上下文环境上关闭**:**即使`variable` `a`只是持有函数`inner``inner`该函数可以访问父函数执行上下文，因为`inner`函数在父函数执行上下文环境上创建了一个闭包，所以我们可以访问在函数范围内声明的参数和变量。**

**关于闭包和它们是什么有很多解释，这是我的，我也可能是错的，所以如果你认为这里有什么完全错了，请评论；)**

# **你可能也会喜欢:**

**[](https://betterprogramming.pub/callbacks-vs-promises-vs-async-await-a-step-by-step-guide-f93d13447604) [## 回调 vs .承诺 vs .异步 Await:逐步指南

### 引擎盖下也有点。

better 编程. pub](https://betterprogramming.pub/callbacks-vs-promises-vs-async-await-a-step-by-step-guide-f93d13447604) [](https://betterprogramming.pub/ec6-magic-you-wish-you-knew-8494da448866) [## 3 个简洁的 Ec6 技巧，加快编码速度

### 你希望知道的魔法

better 编程. pub](https://betterprogramming.pub/ec6-magic-you-wish-you-knew-8494da448866) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***