# 理解 JavaScript 中的调用栈、回调和高阶函数

> 原文：<https://javascript.plainenglish.io/the-call-stack-callbacks-and-higher-order-functions-9191302481a0?source=collection_archive---------6----------------------->

## 理解 JavaScript 的一些较难的部分。

进入 JavaScript 的复杂部分，首先会遇到高阶函数、回调函数和 JavaScript 调用栈。这些看似深奥的东西甚至会让有经验的开发人员出错。所以今天，我将以一种简单的方式来分解这些事情，以便我们在继续我们的 JavaScript 体验之前获得一个坚实的基础。

![](img/937af9c9256bb1ac66e4316730336b73.png)

## 调用堆栈

在讨论调用堆栈之前，我们需要首先了解 JavaScript 如何在我们的代码中运行。JavaScript 有一个“执行线程”，这个执行线程一行一行地执行我们的代码，或者“做”我们的代码。当我们调用一个函数时，执行的线程织入到函数中，在继续执行之前，在函数中要执行代码的地方停下来。(注意:这里假设我们没有做异步代码)

这是调用栈发挥作用的地方:JavaScript 需要跟踪我们的执行线程在哪里&什么函数当前正在运行。需要注意的是，在调用栈的最底层是`global()`函数，它告诉 JavaScript 在没有其他函数运行时继续执行我们的全部代码。

当执行线程到达我们代码中的函数调用时，JavaScript 获取该函数并将其推到调用堆栈的顶部，继续跟踪我们的执行线程在哪里以及它正在执行什么函数。现在这个函数在调用栈的顶部，JavaScript 织入我们的函数，并开始运行调用栈顶部的函数中的代码。一旦我们完成了这个函数，它就从调用栈顶弹出，JavaScript 返回运行下一个最高的操作(在我们的例子中是`global()`)。

假设我们有一个简单的 Math.js 文件，其中包含一些代码和一些数学表达式函数:

```
const num1 = 10
const num2 = 5function multiply(param1, param2) {
 return param1 * param2
}function divide(param1, param2) {
 return param1 / param2
}const product = multiply(num1, num2) // 50
const quotient = divide(num1, num2) // 2
```

当我们运行这段代码时，我们的执行线程从最顶端开始，而`global()`函数位于调用堆栈的顶端。当 JavaScript 随着执行线程一行一行地遍历代码时，它存储我们的常数`num1`和`num2`，我们的函数在内存中乘除，一行一行地执行`global()`函数。

然后我们点击我们的`product`声明。当我们声明`product`时，我们告诉 JavaScript 它评估从函数`multiply`返回的带有参数`(num1, num2)`的内容——因此，我们的执行线程织入乘法，将`multiply(4, 2)`推到调用堆栈的顶部。现在我们在乘法函数内部，JavaScript 停止执行任何其他代码，直到我们从表达式`4 * 2`返回结果，织出乘法函数，将其弹出调用堆栈，并将`product`设置为返回值 8。

最后，我们回到了`global()`函数。JavaScript 移动到下一行，我们重复前面的过程，但是执行线程织入`divide`函数并将`divide`推到调用栈的顶部。一旦`divide`完成运行，我们再次将其从调用堆栈中弹出，并且`quotient`被评估为返回值 2。

## 回调和高阶函数

现在我们对调用堆栈的工作原理有了一点了解，让我们编辑我们的示例 Math.js 文件，并用两个回调函数参数组成我们的高阶函数。但是在我们继续这个例子之前，记住调用栈是很重要的，因为它使得理解高阶函数和回调函数更加容易。

```
const num1 = 10
const num2 = 5function multiply(param1, param2) {
 return param1 * param2
}function divide(param1, param2) {
 return param1 / param2
}function sumOfTwoMathFunctions(callbackOne, callbackTwo) {
 const res1 = callbackOne(num1, num2)
 const res2 = callbackTwo(num1, num2)
 return res1+res2
}const num3 = sumOfTwoMathFunctions(multiply, divide) // 52
```

现在，让我们来看一下运行 Math.js 文件时它发生了什么。我们的执行线程从顶部开始，当我们声明`num1`、`num2`和我们的三个函数时，它保留在我们的`global()`函数中。

但是让我们暂停一下，谈谈我们的第三个功能。你注意到了吗，如果你看声明行，它看起来只是一个普通的函数。高阶函数只是普通的函数，在调用时以其他函数作为参数。哦，那些我们作为参数传递的函数呢？那些是回调函数！

当我们写函数的时候，在我们写完函数之后，我们唯一能在函数内部改变的是我们作为变量留下的内容，当函数被调用的时候，它将被参数填充。但是如果我们想改变一个函数的一些内部功能呢？例如，如果我们写了一个减法函数，我们想要得到`multiply(num1, num2)`和`subtract(num1, num2)`的和。我们所要做的就是将调用`sumOfTwoMathFunctions`时的一个参数改为`subtract`！以上例为基础:

```
sumOfTwoMathFunction(multiply, subtract) // 55
```

在一个函数中留下一些信息“空白”,以便我们的函数可以重用，这是我们都已经知道的事情。但是留下一些*功能*“空白”以使一个函数更加通用&可重用，这就是高阶函数和回调函数发挥作用的地方。

现在我们已经理解了高阶函数和回调函数的原因和方法，让我们继续执行线程吧！一旦我们到达最后一行，我们的执行线程就必须编织到我们新创建的函数中，将`sumOfTwoMathFunctions`推到调用堆栈的顶部。从那里，我们的下一行代码要求我们织入我们的第一个回调函数`multiply`，把它推到栈顶，在我们的`sumOfTwoMathFunctions`函数之上。我们的调用栈现在是这样的，从上到下:`multiply(4, 2)`->-`sumOfTwoMathFunctions(multiply, divide)`->`global()`。正如我们现在所知道的，JavaScript 正在执行我们在`multiply`中的代码，直到我们从其中返回，从调用栈中弹出，允许它移动到我们的下一个回调函数。

虽然这似乎是对调用堆栈的基本解释，但它展示了 JavaScript 如何“读取”和执行我们的代码。理解如何在多层函数中遵循执行线程是理解更复杂主题(如 currying 函数)的关键。

*更多内容请看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***