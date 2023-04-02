# JavaScript 面试问题

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-one-must-know-b3999daa15ce?source=collection_archive---------3----------------------->

## 第 1 章:JavaScript 面试必答问题

![](img/4cf95b3b2285c38a0a238ee6f30c6bb6.png)

Photo by [Blake Connally](https://unsplash.com/es/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是世界上最流行的编程语言，被广泛用于 web 开发。具有 JavaScript 背景的开发人员可以很容易地接触到 React 等前端库。

这使得 JavaScript 成为专业人士的必备语言。由于 JavaScript 的广泛使用，它为新生/专业人士提供了大量的工作机会。如果你正在准备 JavaScript 面试，下面是你必须知道的问题列表。

1.  **JavaScript 中异步代码如何执行？**

JavaScript 只有一个调用栈和一个内存堆。它按照代码定义的顺序执行代码，这意味着 JavaScript 本质上是同步的。当我们从服务器获取数据或使用 ajax 调用时，这种同步特性可能会导致问题。

**回调或承诺**用于处理这种异步行为。像承诺这样的异步操作被保存在队列中。这个事件队列将在主线程完成处理后运行(因为 JavaScript 是单线程的)。这将防止任何后续的封锁。一旦执行完成，promise 将把结果返回给 JavaScript 环境。

**2。JavaScript 是单线程语言吗？**

是的，JavaScript 是单线程语言，因为它只有一个调用栈。

**3。调用、应用和绑定之间的区别？**

**调用():**

call()方法用于调用函数，该值作为第一个参数和自变量提供。call 方法单独接受参数/用("，")分隔。

**应用():**

与 call()方法类似，apply()也用于调用具有给定值的函数。唯一的区别是 applying 方法接受数组中的参数。

**bind():**

bind()方法使用提供的值和上下文绑定函数。它不会在绑定后立即调用函数，函数调用需要单独调用。它将返回新的函数。

**区别:**

*   `call()`和`apply()`做相同的函数调用工作，唯一的区别是 call 分别接受参数，而 apply 接受数组中的参数。
*   `bind()`将返回一个新功能。call 和 apply 不返回新函数，它们根据提供的值调用函数。
*   `call()`和`apply()`会立即调用函数，bind 不会立即调用函数。

Apply

Call

Bind

**4。承诺的状态是什么？**

**承诺:**

承诺提供了一种更干净的方式来处理异步操作。正如诺言这个词所暗示的，它要么在未来被遵守和履行，要么被打破。JavaScript 中的 Promise 有三种状态——已解决、待定和已拒绝。

*   **待定状态:**创建承诺后，在解决或拒绝之前，它将处于待定状态。例如，当我们发布一个从服务器获取数据的请求时，它处于挂起状态，直到被接收。
*   **已解决:**执行成功。例如，从服务器请求的数据被成功接收。你可以用。然后()进一步执行。
*   **拒绝:**执行失败。例如，由于网络错误而无法接收数据。你可以用。catch()来处理这种情况。

**5。什么是 JavaScript 全局变量？**

JavaScript 中的全局变量是在函数外部声明的，也可以用窗口对象声明。它们在整个程序中都是可访问的。
如果你正在处理大型代码，最好使用最小的全局变量，因为它们会因为相同的变量名而产生不明确的行为。

JavaScript Global Variable Example

**6。箭头功能是什么？箭头函数和普通函数有什么区别？**

Arrow 函数让我们对函数声明使用更简单的语法。
与正常功能相比，

*   箭头函数很容易写。
*   **该**关键字与箭头功能无关。

Arrow Function Example

本文到此为止。如果你觉得这篇文章有帮助，那么请检查其他文章！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***