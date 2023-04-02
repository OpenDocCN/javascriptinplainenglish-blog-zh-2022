# 我们每天都在做的 JavaScript 反模式

> 原文：<https://javascript.plainenglish.io/javascript-anti-patterns-we-do-every-day-3d0086e2910?source=collection_archive---------0----------------------->

## JavaScript 开发人员经常犯的最常见错误——您应该避免这些错误，以编写干净、合理和正确的代码。

编写代码很容易，但编写干净、合理和正确的代码是一种棘手的技能，我们需要通过熟悉大量代码和最佳实践来发展。在本文中，我们将看看 JavaScript 开发人员最常犯的错误。

![](img/c95b916c24cfe76a7c3883a78844d6a5.png)

Credits to [Performance Management Company Blog](https://performancemanagementcompanyblog.wordpress.com/)

# 什么是反模式？

想象一下，你是一名战争中的士兵&你应该用枪和与军队相关的东西杀死你的敌人，但你选择用剪刀杀死你的敌人，最终你可能杀死你的敌人，实现你的目标和加入战争的理由，但你以错误的方式这样做！你让这项工作变得更难、更乱、更没有条理。

这在软件工程世界中几乎是一样的，你可能每天都在做这件事，却没有真正被告知，我将帮助你在 JS 中找到这些反模式。

请注意，我们不能在这里指出 JS 的所有反模式，因为它实际上是基于你和你是多么糟糕和不研究的家伙。如果你研究得不够好，你的代码库中会有越来越多的反模式。:)

## 1.JavaScript 循环

我可以肯定地说，我们在代码中犯的最常见的反模式与循环相关的事情和错误地选择 **for…of、forEach 和 map 有关。**

让我们从一个糟糕的 JS 地图用法开始:

```
[1,2,3].map(i => console.log(`Logged to console ${i} times`))// log
Logged to console 1 times
Logged to console 2 times
Logged to console 3 times
```

看，我们从这个循环中得到了正确的输出和行为！那到底怎么了？

JavaScript map 是一个数组方法，用于循环遍历一个数组，并将一个数组作为输出和结果返回给您！根据 MDN 的描述，`**`**map()**`**方法创建一个新的数组，其中填充了对调用数组中的每个元素调用所提供的函数的结果。这意味着当你想要一个数组作为输出时，你可以像下面的例子一样使用这个方法:****

```
const myArray = [1, 4, 9, 16];const myMap = myArray.map(x => x * 2);console.log(myMap);
// expected output: Array [2, 8, 18, 32]
```

**那么登录控制台 5 次是什么模式呢？当你在思考这个问题的时候，你记起了你以前在代码中记忆和使用过的一个方法或 HOF，请简单地搜索和阅读官方网站的文档，看看这个方法的目的是什么，以及如何以你能做到的最好的方式使用它，例如，我们可以简单地用 JavaScript 中的 for…of 登录控制台**

```
for (let step = 0; step < 3; step++) {
  // Runs 3 times
  console.log(`Logged to console ${step + 1} times`)
}// log
Logged to console 1 times
Logged to console 2 times
Logged to console 3 times
```

## **2.常量、变量和 let**

**看起来很简单，不是吗？如果您在使用它们之前没有阅读它们的用途和文档，请确保您在这方面也犯了一个错误。**

**与循环部分不同，这个主题更容易学习和适应最佳实践。**

**首先是棘手的`var`关键字，该语句将声明一个函数作用域或全局作用域的变量，由于提升行为，不建议在局部作用域变量中使用它。并且它们是在任何代码执行之前被处理的，所以您可能会犯错误，直到应用程序运行时才注意到它们。这可能需要几个小时的调试，因为你不会得到一个未定义的错误，而是一个未定义的变量值！**

```
{ 
   var greeting= "Hello" 
}console.log(greeting);// log
Hello !!!!!!!!
```

**那怎么办呢？这里只需简单地使用块范围的关键字，如 **const** 和 **let。****

```
{ 
   let greeting= "Hello" 
}console.log(greeting);// log
Uncaught ReferenceError: greetings is not defined
```

**好了，现在我们从 var 开始，还没轮到`const`和`let`，这里的规则很简单，只是请不要使用`let`来声明不应该在将来编辑和更改的变量，你可能会说，**“好吧，我不会给它赋值和编辑，但为什么不在这里使用** `**let**` **？”这正是人们在代码中生成反模式的原因。****

```
// Correct
const THIS_VARIABLE_WILL_NOT_CHANGE = "JS is not weird";// Wrong
let THIS_VARIABLE_WILL_NOT_CHANGE = "JS is not weird";
```

## **3.U `nnecessary nesting`**

**这个话题有点复杂，在某些方面可能有点抽象，因为我们可能在不同的条件下面临这个错误，但让我们看看其中的一些！**

**在**承诺下使用许多嵌套步骤可能会使你的代码变得混乱和反模式。让我用一个例子来说明这一点:****

```
// Bad example! Spot 3 mistakes!

doSomething()
  .then(function (result) {
    // Forgot to return promise from inner chain
    // unnecessary nesting doSomethingElse(result)
      .then((newResult) => doThirdThing(newResult));
  })
  .then(() => doFourthThing());
// Forgot to terminate chain with a catch!
```

**现在让我们让这个错误的例子看起来正确并且模式友好:**

```
doSomething()
  .then(function (result) {
    return doSomethingElse(result);
  })
  .then((/* result ignored */) => doFourthThing())
  .catch((error) => console.error(error));
```

**你可以从 MDN 文档中了解更多[承诺常见错误。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises#common_mistakes)**

**当你忘记 JavaScript 中的`return`和`break`时，通常会发生其他不必要的嵌套事情！**

```
function is_old_aged(age) {
  if (age) {
     if (age > 60) { 
      return 'old' 
     } else {
      return 'young'
     };
  }
}
```

**我讨厌这些嵌套层次的条件，因为你的代码在 2 层嵌套条件后会变得很糟糕，而且没有人能肯定地读懂你的代码，但是该怎么办呢？**

```
function is_old_aged(age) { if (!age) {
     return false;
  } return age > 60 ? 'old' : 'young'
}
```

**干净多了，不是吗？**

# **包扎**

**正如我在开始时提到的，本文的主要观点并不是指出编写 JavaScript 代码的所有错误和反模式，而是鼓励您在编写代码之前研究、阅读并渴望了解编程语言模式的主要用途。您可以通过从可靠来源或官方文档中学习来做到这一点。**

**你可以在 [MDN 官方网站](https://developer.mozilla.org/en-US/)上阅读更多关于所有 JavaScript 函数和方法的内容。**

**你可以通过下面的链接阅读我的其他文章:**

**加速 JS:**

**[](/how-i-make-my-javascript-applications-2-times-faster-dbbfd7e5ceec) [## 我如何让我的 JavaScript 应用程序速度提高两倍

### 在本文中，我们将快速浏览一下可以用来尽快创建 web 应用程序的技巧。

javascript.plainenglish.io](/how-i-make-my-javascript-applications-2-times-faster-dbbfd7e5ceec) 

核心网络要素:

[](/core-web-vitals-boosting-your-websites-speed-a2ea4d595f0d) [## 核心网站要害&提高网站速度！

### 在这篇文章中，我们将快速浏览一下 web 关键点&使用它们来提高我们的 Web 应用程序性能

javascript.plainenglish.io](/core-web-vitals-boosting-your-websites-speed-a2ea4d595f0d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****