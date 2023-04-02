# 使用程序模板学习 JavaScript

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-dca7ea7adc96?source=collection_archive---------19----------------------->

## 第 2 部分:从备选方案中选择

![](img/d92d1a70b532299c717d8358d24332ce.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在早先的[文章](/learn-javascript-with-program-templates-select-from-alternatives-d4f9270f3fac)中，我讨论了如何使用 JavaScript 来实现使用不同形式的`if`语句的 *Select From Alternatives* 程序模板。在本文中，我继续使用嵌套的`if` 语句和`switch`语句来实现这个模板。让我们开始吧。

# 使用嵌套的 if 语句从备选项中进行选择

通常，从备选方案中进行选择需要先做出一个重大决策，然后才能做出其他不太重要的决策。实现这种决策的最佳方式是使用嵌套的`if`语句。

让我们从一个简单的银行贷款申请开始。获得银行贷款的第一个要求是你必须每年至少挣 25000 美元。然后，如果你符合这个要求，你也必须已经工作了至少两年，至少有体面的信用。下面的程序演示了如何编写嵌套的 if 语句来实现这种情况:

```
putstr("Enter your salary: ")
let salary = parseFloat(readline())
if (salary >= 25000) {
  putstr("Enter your length of employment at current job: ")
  let employ = parseInt(readline())
  putstr("What is your credit (Poor, Fair, Good, Excellent)? ")
  let credit = readline()
  if (employ >= 2 &&
       (credit == "Good" || credit == "Excellent")) {
    print("You can be considered for a loan.")
  }
  else {
    print("Sorry, you must be employed at your current job for")
    print(" at least 2 years and you must have good or")
    print(" excellent credit to be considered for a loan.")
  }
}
else {
  print("Sorry, you must make at least $25,000 to be ")
  print(" considered for a loan.")
}
```

下面是这个程序的一些运行，测试每个可能的场景:

```
Enter your salary: 25001
Enter your length of employment at your current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Good
Sorry, you must be employed at your current job for at least 2 years
and you must have good or excellent credit to be considered
for a loan.Enter your salary: 25001
Enter your length of employment at your current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Good
You can be considered for a loan.Enter your salary: 25001
Enter your length of employment at current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Fair
Sorry, you must be employed at your current job for at least 2 years
and you must have good or excellent credit to be considered
for a loan.Enter your salary: 24999
Sorry, you must make at least $25,000 to be considered for a loan.
```

# switch 语句

使用`if` 语句实现*从备选项中选择*模板的另一种方法是`switch`语句。`switch`语句是一个更加结构化的语句，当程序需要选择的选项被表示为单个值而不是范围时，它工作得很好。

switch 语句的语法模板如下所示:

```
*switch(expression) {
 case (value):
 case body;
 break;
 case (value):
 case body;
 break;
 …
 default:
 default body;
}*
```

一个例子将有助于弄清楚`switch`语句是如何工作的。质量分用于计算学生的平均绩点(GPA)。A 值 4 个质量点，B 值 3 个质量点，C 值 2 个质量点，D 值 1 个质量点，F 值 0 个质量点。以下程序要求用户输入课程的字母等级，然后确定质量分数:

```
let totalPoints = 0
putstr("What is the letter grade for the course? ")
let grade = readline()
switch(grade) {
  case "A":
    totalPoints += 4
    break
  case "B":
    totalPoints += 3
    break
  case "C":
    totalPoints += 2
    break
  case "D":
    totalPoints += 1
    break
  case "F":
    totalPoints += 0
    break
default:
  print("Unknown value")
}
print("A grade of",grade,"is worth",
  totalPoints,"quality points.")
```

以下是该程序几次运行的输出:

```
What is the letter grade for the course? B
A grade of B is worth 3 quality points.What is the letter grade for the course? C
A grade of C is worth 2 quality points.What is the letter grade for the course? A
A grade of A is worth 4 quality points.
```

`switch`语句的另一个常见用法是实现一个菜单。下面的程序演示了一个用于执行简单计算的菜单系统。程序如下:

```
print("Simple Calculator")
print()
print("1\. Addition")
print("2\. Subtraction")
print("3\. Multiplication")
print("4\. Division")
print()
putstr("Enter your choice: ")
let choice = parseInt(readline())
let op1, op2
switch (choice) {
  case 1:
    putstr("Enter operand: ")
    op1 = parseInt(readline())
    putstr("Enter operand: ")
    op2 = parseInt(readline())
    let sum = op1 + op2
    print("The sum of",op1,"and",op2,"is",sum)
    print()
    break
  case 2:
    putstr("Enter operand: ")
    op1 = parseInt(readline())
    putstr("Enter operand: ")
    op2 = parseInt(readline())
    let difference = op1 - op2
    print("The difference of",op1,"and",op2,"is",difference)
    print()
    break
  case 3:
    putstr("Enter operand: ")
    op1 = parseInt(readline())
    putstr("Enter operand: ")
    op2 = parseInt(readline())
    let product = op1 * op2
    print("The product of",op1,"and",op2,"is",product)
    print()
    break
  case 4:
    putstr("Enter operand: ")
    op1 = parseInt(readline())
    putstr("Enter operand: ")
    op2 = parseInt(readline())
    let quotient = op1 / op2
    print("The quotient of",op1,"and",op2,"is",quotient)
    print()
   break
}
```

以下是该程序的一些运行情况:

```
Simple Calculator1\. Addition
2\. Subtraction
3\. Multiplication
4\. DivisionEnter your choice: 3
Enter operand: 12
Enter operand: 2
The product of 12 and 2 is 24Simple Calculator1\. Addition
2\. Subtraction
3\. Multiplication
4\. DivisionEnter your choice: 2
Enter operand: 12
Enter operand: 3
The difference of 12 and 3 is 9
```

# 最后的想法

我已经向您展示了实现 *Select From Alternatives* 程序模板的两种替代方法——嵌套的 if 语句和 switch 语句。稍后，当我谈到数组数据结构时，我将向您展示如何使用一种叫做表查找的东西来实现这个模板。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*