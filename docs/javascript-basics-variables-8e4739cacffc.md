# JavaScript 基础:变量

> 原文：<https://javascript.plainenglish.io/javascript-basics-variables-8e4739cacffc?source=collection_archive---------16----------------------->

## 回顾与变量相关的所有事情:命名约定、var vs let、提升以及使用哪种类型

![](img/d595400202bc1e61b4192989e445e1d5.png)

Photo by [Sergi Kabrera](https://unsplash.com/@skabrera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当开始学习 JavaScript 时，变量是最先涉及的事情之一(紧接在明显的:`console.log("Hello World");`)之后。它们是构建其他一切的基础组件。

虽然这是一个可以略过的基本话题，但我个人认为花时间在基本的构建模块上对以后的成功至关重要。奠定基础的早期工作永远不会被浪费，因为它是更复杂主题的基础。

这就是为什么这篇文章致力于变量的不同方面。从如何创建它们开始，并决定分配哪个名称，然后继续查看不同的可用类型、可变范围，最后是提升。

# 宣布或分配

创建变量时，我们有两种选择。我们可以创建变量并赋予它一个初始值，例如:

```
var name = "Stef";
```

或者，我们只声明变量并将其值留空，以便稍后在代码中赋值，例如:

```
var numOfStudents;
```

*注意:当使用* `*const*` *变量类型时，你不能声明必须被赋值的变量——原因将在后面的部分解释。*

# 命名变量

关于 JavaScript，需要注意的一点是变量都是区分大小写的，例如:

```
*//Create the variable name*
var name = “Stef”;*//Request to print the variable*
console.log(name); // Returns Stef*//Request to print the variable with it written in title case*
console.log(Name); // Returns an error: Name is not equal to name
```

虽然您可以随意命名变量，但是有几个约定应该遵守，以便您的代码可以被其他人理解:

1.  **不允许空格**
    变量名必须是没有任何空白字符的单个文本字符串
2.  **用 camelCase** 写
    当一个变量名包含多个单词时，惯例是使用“camelCase”。Camel case 涉及从小写字母开始，然后将每个后续单词的第一个字母大写。
3.  **变量名应该是描述性的** 一个阅读你的代码的人应该明白变量包含什么数据，而不需要注释。因此，变量名应该具有足够的描述性，以便于理解正在发生的事情。

# var' vs 'let' vs 'const '

历史上，在 JavaScript 中设置变量只有一种方法，那就是使用`var`语法。然而，当 ES6 更新发布时，增加了两个选项`let`和`const`。让我们来看看这些，以及在工作中使用正确的关键词的好处。

*   **const** 适用于不会改变的变量。如果你知道一个值应该在整个项目中保持固定，建议使用 *const* 来防止对变量的意外和不必要的改变。因为它们不可更改，所以在创建变量时必须赋值。
*   **let** 是一个变量的新 ES6 语法，可以在脚本运行过程中改变。当引入一个新的 *let* 变量时，它可以被赋值也可以被声明。 *let* 变量是块范围的(在下面的变量层次结构一节中有更多相关内容)
*   **var** 是遗留变量语法。与 *let 一样，*它可以在脚本运行过程中更改。 *let* 和 *var* 的一个主要区别是 *var* 具有全局范围。也可以重新声明 *var* 一些在使用 *let* 时不可能的事情

```
**//var can be redeclared**
var a = 4;
var a = 5:
**//let cannot be redeclared**
let a = 4;
let a = 5; //Throws an error
**//Both can be reassigned as needed** var a = 5;
let b = 4;
a = 3;
b = 6;
```

# 可变层次结构

在上一节中，提到了 *var* 和 *let* 以类似的方式操作，除了 *var* 具有全局范围而 *let* 具有块范围，但是这实际上意味着什么呢？

用一个例子更容易理解。声明的任何 *let* 变量仅在声明它的特定块中可用:

```
function welcome() {
   let a = "Hi!"
   if (a == "Hi!") {
        let b = " Welcome!"
        console.log(a + b) **//Returns "Hi! Welcome!"** }
   console.log(a + b)    **//An error is returned. b is not accessible**
}
welcome()
```

而当使用 *var* 时，该变量在整个函数中都可用:

```
function welcome() {
   var a = "Hi!"
   if (a == "Hi!") {
        var b = " Welcome!"
        console.log(a + b) **//Returns "Hi! Welcome!"** }
   console.log(a + b)    **//Also returns "Hi! Welcome!"**
}
welcome()
```

# 提升

提升是在声明变量之前使用变量的地方。 *var* 支持吊装，而 *let* 不支持吊装。就我个人而言，我尽量避免这种做法，因为它会使代码难以阅读，但这是值得注意的，因为我们正在研究不同类型之间的差异。

```
**//Hoisting a var variable**
console.log(a); // Will return 'undefined' but not an error
var a;**//Attempting to hoist a let variable, an error will be returned**
console.log(a); // Returns 'Uncaught ReferenceError' 
let a;
```

# 摘要

我希望它对您的编码之旅有所帮助，并帮助您澄清关于如何正确使用 JavaScript 中的变量的任何问题。虽然一个简单的概念使用正确类型的变量并正确命名它们对于编写高效和可读的代码很重要。

> ***感谢阅读！如果你喜欢这个帖子并想阅读更多，请务必查看我的个人资料或订阅类似帖子的***[](https://medium.com/subscribe/@simply_stef)****。****
> 
> *订阅 Medium 可以无限制地获取所有可用的内容和想法。 [***如果你通过这个链接加入 Medium，我会从你的费用中收取很少的一部分——而且不会花你任何额外的费用！***](https://medium.com/@simply_stef/membership)*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。****