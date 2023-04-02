# JavaScript 中的“if-else”条件语句

> 原文：<https://javascript.plainenglish.io/the-if-else-conditional-statement-in-javascript-474e4f6d8aa8?source=collection_archive---------11----------------------->

## 这就是编程的意义所在。

![](img/8f130a16110342d50848d8b3c3dd2e06.png)

Photo on Unsplash by [https://unsplash.com/@reskp](https://unsplash.com/@reskp)

比尔·盖茨曾经说过，“计算机编程就是数学计算和用 if 做决策..否则”。

很难反驳这种说法，为什么不。因为在内心深处这就是编程的意义所在。

如果你是这个编程世界的新手，可以考虑通读这篇文章:[编程时要学的 3 件事](https://withinbracket.com/posts/3-things-to-learn-while-programming/)以获得更好的参考。

[https://medium . com/nerd-for-tech/3-things-to-learn-while-programming-2e 9 b42 D8 b 014](https://medium.com/nerd-for-tech/3-things-to-learn-while-programming-2e9b42d8b014)

无论如何，如果你从事计算机编程已经有一段时间了，你可能知道程序是建立在`logics`之上的。而逻辑需要经过一定的条件才能满足某个特定的问题。

这就是`conditional statements`的用武之地。他们帮助我们做出解决问题的决定。

一般将`conditional statements`简称为`if...else`。它们非常简单明了:

```
if(this happen){
   do this particular task;
}else{
   do this.
}
```

这意味着，如果`certain`条件满足，就做一个**特定的**任务，如果条件不满足，就做**别的**事情。

# 看看这个简单的例子:

```
let num = 1;if(num > 0){ 
   console.log("The number is positive");
} else {
   console.log("The number is negative");
}
```

# 条件语句的类型

在任何编程语言中，通常存在两种类型的条件语句:

*   如果…否则
*   否则如果

让我们分别来看看:

# 如果…否则

语法:

```
if(this condition satisfies){
        do a particular task
    } else {
        do something else.
    }
```

这个语法类似于我们之前讨论的。如果一个条件`satisfies`，做一个**特定的**任务，否则，做别的。

示例:

```
// Check if a number is odd or even
    let num = 7;
    if(num % 2 == 0){
        console.log("The number is even");
    } else {
        console.log("the number is odd");
    }
```

在上面的例子中，我们已经检查过，当一个数除以 2 时，如果我们得到`0`作为**余数**，那么这个数就是`even`，如果我们得到`1`作为余数，那么这个数就是`odd`。

**注:** '% '是**模运算符**，它在除数时给出`reminder`，而'/'给出`quotient` 。

# 否则如果

除了`if...else`，我们还有`else if`，用来增加另一个**条件**。

语法:

```
if(this condition satisfies){
   do a particular task
} else if(check this condition){
   do this task
} else {
   do something else.
}
```

在这个语法中，你可以很容易地看到这里还有一个`condition`要检查。

在`else if`的帮助下，我们可以添加想要检查的任意多个条件。

示例:

```
let num = 5;if(num > 0){
   console.log("The number is positive");
} else if(num == 0){
   console.log("The number is ZERO");
} else {
   console.log("The number is negative");
}
```

***相当明显；*** 在上面的程序中我们还检查了这个数字是否是`0`，并使用`else..if`打印出与那个`condition`相关联的`log`语句。

# 嵌套条件

到目前为止，我们已经了解了什么是条件语句及其类型。但是我们有另一种类型的条件语句，即**嵌套**。

嵌套意味着检查特定条件内的条件**。**

*有道理吗？检查这个例子:*

```
let num1 = 5;
let num2 = 8; if(num1 == num2){
    console.log("Both number are equal");
} else {
    if(num1 > num2){
       console.log("num1 is greater than num2");
    } else {
       console.log("num1 is lesser than num2");
    }
}
```

在上面的例子中，我们有一个`if..else`语句。但是在`else`块中，我们有另一个`if..else`语句。这被称为嵌套条件语句。

# 要记住的事情:

这里我们已经学习了条件语句，但是在使用它们的时候，你需要考虑一些事实。

*   `else`后面总是应该跟着一个`if`语句
*   仅当您需要检查其他情况时，才使用`else if`
*   如果`else`完成了你的工作，`else if`可能不需要添加

# 结论

所以让我们总结一下。在任何编程语言中，我们都有两种条件语句:

*   如果...其他
*   否则如果

我们还有一个嵌套的条件语句，用于检查条件中的条件。

这就是 JavaScript 中的条件语句。

**这篇文章正式发表在括号内:**

[](https://withinbracket.com/posts/if-else-in-javascript-conditional-statement/) [## 在 JavaScript 条件语句中

### 这就是编程的意义所在。比尔·盖茨曾经说过，“计算机编程是数学计算和制作…

withinbracket.com](https://withinbracket.com/posts/if-else-in-javascript-conditional-statement/) 

# 关于 JavaScript 的更多信息

[](https://withinbracket.com/posts/data-types-in-javascript-the-weird-parts/) [## JavaScript 中的数据类型——奇怪的部分

### 你需要知道的编程核心概念。如果你对编程有一段时间了，你知道什么是…

withinbracket.com](https://withinbracket.com/posts/data-types-in-javascript-the-weird-parts/) [](https://withinbracket.com/posts/variables-in-javascript-scope-and-hoisting/) [## JavaScript 中的变量、范围和提升

### 编程的核心概念，一个都不能跳过。变量是任何事物最基本也是最重要的部分…

withinbracket.com](https://withinbracket.com/posts/variables-in-javascript-scope-and-hoisting/) [](https://withinbracket.com/posts/type-conversion-in-javascript-the-magic/) [## JavaScript 中的类型转换——魔法

### 不仅仅是数据类型。如果你是一个 JavaScript 开发者，那么你必须知道 JavaScript 有三种基本类型…

withinbracket.com](https://withinbracket.com/posts/type-conversion-in-javascript-the-magic/) [](https://withinbracket.com/posts/loops-in-javascript/) [## JavaScript 中的循环介绍

### 用 loop 做一些重复的任务不管你是属于哪种编程语言还是哪种编程语言…

withinbracket.com](https://withinbracket.com/posts/loops-in-javascript/) [](https://withinbracket.com/posts/javascript-equality-double-equals-vs-triple-equals/) [## JavaScript 等式-两倍等于(==)和三倍等于(===)

### 这里是大多数人犯错的地方。所以你最好不要。在任何编程中，我们作为程序员经常做的一件事是…

withinbracket.com](https://withinbracket.com/posts/javascript-equality-double-equals-vs-triple-equals/) 

谢谢你留下来。不断学习。

📌点击此处查看更多文章:

[](https://withinbracket.com/archives/) [## 在括号内-特色文章

### 以下是括号内的文章。

withinbracket.com](https://withinbracket.com/archives/) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*