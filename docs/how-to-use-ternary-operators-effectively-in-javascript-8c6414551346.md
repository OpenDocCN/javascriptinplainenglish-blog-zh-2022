# 如何在 JavaScript 中有效使用三元运算符

> 原文：<https://javascript.plainenglish.io/how-to-use-ternary-operators-effectively-in-javascript-8c6414551346?source=collection_archive---------9----------------------->

## 如何在 JavaScript 中有效使用三元运算符的教程。

![](img/cd7bfc2df9fd16d61a984ecf47c247ea.png)

# 介绍

在本文中，我们将了解如何有效地使用三元运算符，但在此之前，我们需要了解三元运算符，所以让我们先探索一下，然后我们将讨论我们的主要话题。

因此，三元运算符用于替换任何语句中的 if-else 条件。换句话说，它允许我们在一行中为 if-else 条件编写代码，实质上缩短了 if-else 条件。条件运算符是唯一接受三个操作数的 Javascript 运算符。让我们检查下面给出的语法。

```
Condition ? expression1  : expression 2
```

这里我们必须理解三个概念:表达式 1、表达式 2 和条件。所以我们来理解一下这个。这里的三元运算符将检查条件，并根据该条件运行表达式。它可以是 expression1 或 expression2，但不可能同时运行。现在让我们探索一下哪个表达式将在什么时候运行。

*   如果条件为真，那么将执行表达式 1。
*   如果条件为假，那么将执行表达式 2。

正如我们在这里看到的，三元运算符有三个操作数；因此，它的名字是三元的。三元运算符也称为条件运算符。让我们借助一个例子来理解这一点。

```
var age = 30;
var drink = (age > 21) ? “Alcohol” : “Juice”;
console.log (drink);
```

现在让我们来理解这段代码。这里我们定义了一个值为 30 的变量。在这段代码中，我们要检查一个人是否有资格喝酒。所以我们提出了一个条件，21 岁以上的人有资格，其余的人没有资格。所以，在第二行，我们把我们的条件:年龄> 21。如果我们的可变年龄满足它，它将返回“酒精”，否则它将返回“果汁”，我们可以使用 console.log()打印它。

让我们借助另一个例子来更清楚地理解。

```
const answer = (result) => {
return result > 33 && result < 100 ? “Pass”
: result < 33 && result > 0 ? “Fail”
: “inappropriate marks”;
}
console.log (answer (49));
console.log (answer (20));
console.log (answer (-12));
```

**输出将是:**

```
Pass
Fail
Inappropriate marks
```

现在让我们探索一下，如果我们必须在 if-else 条件下编写上面的代码，那么我们应该如何编写，如下所示。

```
const answer = (result) => {
if (result > 33 && result < 100) {
     return “Pass”;
     }
else if (result < 33 && result > 0) {
     return “Fail”;
     }
else {
     return “Inappropriate marks”;
     }
}
```

# 三元运算符和 if-else

我们来探讨一下 if-else 条件和三元运算符有什么区别。让我们借助一个例子来理解这一点。

```
Let age = 10;
Let answer;
If (age >= 18){
     answer = “You are eligible to vote.”
} else {
     answer = “You are not eligible to vote.” 
}
console.log (answer);
```

上面的代码是用 if-else 条件编写的，它将检查一个人是否有资格投票。如果年龄大于 18 岁，那么这个人就有投票权。如果年龄不到 18 岁，那么他或她就没有投票权。让我们使用三元运算符编写相同的代码。

```
let age = 10;
let answer = (age >= 18) ? “You are eligible to vote.” : “You are not eligible to vote.”;
console.log(answer);
```

两者的输出结果将是相同的，两者之间唯一的区别是他们的书写方式。三元运算符将缩短代码。

# 为什么是三元运算符？

JavaScript 中的三元运算符用于缩短代码。在使用三元运算符时，我们可以跳过 if-else 条件。在三元运算符的情况下，代码审查将很容易，理解代码也相对容易。

众所周知，我们可以在 if-else 条件中使用多个 if。同样，我们可以在三元运算符中这样做。让我们借助下面给出的例子来理解这一点。

```
let age = 50;
let message = age >= 80 ? “not applicable” : age < 21 ? “not applicable” : “applicable”;
console.log(message);
```

这里年龄是 50，我们应用了两个如果条件，即年龄大于等于 80，那么不适用；如果年龄小于 21 岁，则同样不适用；否则它将是适用的。在这里，三元运算符帮助我们用更少的单词编写代码，也很容易理解。

# 结论

现在，读完这篇文章后，我们可以得出结论，JavaScript 中的三元运算符非常有用，因为它缩短了代码，而且易于理解。

要更深入地了解 JavaScript，请阅读关于 [Scaler 主题](https://www.scaler.com/topics/javascript/)的文章。

*更多内容看**[***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**