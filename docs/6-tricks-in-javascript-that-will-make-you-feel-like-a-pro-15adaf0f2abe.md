# JavaScript 中的 6 个技巧会让你感觉像个专业人士

> 原文：<https://javascript.plainenglish.io/6-tricks-in-javascript-that-will-make-you-feel-like-a-pro-15adaf0f2abe?source=collection_archive---------3----------------------->

## 有了这些简单的命令和技巧，您将能够毫不费力地用 JavaScript 创建非常酷的东西！

![](img/465f5c9651fa321432fe62a685bb0e98.png)

Photo by [Obie Fernandez](https://unsplash.com/@obiefernandez?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript 是世界上最流行的编程语言，它的流行程度只会随着时间的推移而增加。它通常用于前端和后端开发，然而，有许多库、框架和虚拟环境可以让你构建任何你想要的东西。

例如，使用 React Native，你可以同时为 iOS 和 Android 创建一个移动应用程序，正如你所理解的那样，它大大提高了你的效率。所以，是的，JavaScript 现在有点吃香，了解我将在本文中向您展示的技巧将非常有用，尤其是如果您想给某人留下深刻印象的话。继续读，知道一堆新东西！

# 1.箭头功能

当然，列表上的第一个技巧是箭头函数，如果你不知道它，那么你肯定需要知道。这样，你就可以用一种更高效、更简单的方式来编写你的函数，这样你的代码就会减少一半。此外，阅读和理解你的代码会更容易。参见示例:

```
//Usual Functionhello = function(val) {
  return "Hello World!" + val;
}//Arrow Functionhello = (val) => "Hello " + val;
```

# 2.转换为字符串、数字、布尔值

将不同类型的数据转换成另一种类型在许多特定情况下可能非常有用，或者当您只需要转换它以便以后可以将其与其他类型的数据连接时。这里你可以看到它们的例子:

```
//Converting to a stringlet x = 1 + "";
console.log(x); // Result: "1"//Converting to a numberlet y = "25";
y = +y;
console.log(y); // Result: 15//Converting to a booleanconst z = !0;
console.log(typeof z); // Result: "boolean"
```

# 3.Math()运算符的替换

Math()运算符非常有用，有了它，您可以编写非常难的数学算法，并充分利用数学的力量。然而，如果你想做一些简单的任务，如供电和四舍五入，使用普通的 JS 会更好更有效，不需要任何库。看看这个例子:

```
//Powering::Beforeconsole.log(Math.pow(2,3)) //Result: 8//Powering::afterconsole.log(2 ** 3) //Result: 8
```

此外，如果你想四舍五入，也有一个快速的解决方案。你再也不需要用`Math.floor()`、`Math.ceil()`或者`Math.round()`来舍入了，这里就是:

```
//Rounding::Beforeconsole.log(Math.floor(47.6)) //Result: 47//Rounding::afterconsole.log(47.6 | 0) //Result: 47
```

# 4.快速控制台. log

如果你一直在写`console.log()`的全文，那么相信我，我会用这个非常简单的技巧帮你节省很多时间:

```
let c = console.log.blind(document);c("Hello World"); //Result: "Hello World"
c(123); //Result: 123
c(True); //Result: True
```

# 5.删除最后的数字

您还可以使用“or”运算符来删除整数末尾的任意位数。这意味着你不必仅仅为了从整数中删除一个数字而写一长串代码。参见示例:

```
//Beforelet str = "2022"; 
Number(str.substring(0, str.length - 1)); //Result: 202//Afterconsole.log(2022 / 10   | 0)  // Result: 202
console.log(2022 / 100  | 0)  // Result: 20
console.log(2022 / 1000 | 0)  // Result: 2
```

# 6.数字分隔符

如果你在处理长数字，并且总是试图理解它是 1，000，000 还是 10，000，000，那么总会有一个问题，因为没有人知道这种方法可以让你的数字更易读、更美观。在本例中，我们将使用“_”作为数字分隔符:

```
//Beforelet x = 1000000
let y = 10000000//Afterlet x = 1_000_000
let y = 10_000_000//The output will be the same for the both example
```

# 结论

就这样，现在你知道了 JavaScript 的 6 个关键技巧和提示，它们不仅会提高你的生产力，而且在很多情况下会很有帮助，会让你的代码更容易阅读。我试图找到最伟大的，并告诉你，如果你喜欢这篇文章，那么不要忘记在 Twitter 上关注我，并留下掌声！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*