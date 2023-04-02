# 使用程序模板学习 JavaScript:从备选方案中选择

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-select-from-alternatives-9496da0e3c8c?source=collection_archive---------21----------------------->

## 第二部分:使用嵌套的`if`语句和`switch`语句。

![](img/bbf61b2e2b781ed2b9b8186567915561.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在之前的一篇[文章](/learn-javascript-with-program-templates-select-from-alternatives-d4f9270f3fac)中，我讨论了如何使用不同形式的`if`语句，使用 JavaScript 来实现*从备选方案中选择*程序模板。在本文中，我继续使用嵌套的`if`语句和`switch`语句来实现这个模板。让我们开始吧。

# 使用嵌套 if 语句从备选方案中选择

通常，从备选方案中选择需要在做出其他不太重要的决定之前做出一个重大决定。实现这种类型的决策的最好方法是使用嵌套的 if 语句。

让我们从一个简单的银行贷款申请开始。获得银行贷款的第一个要求是，您必须每年至少赚 25，000 美元。然后，如果您符合这个要求，您还必须工作了至少两年，并且至少有可观的信用。下面是一个程序，演示如何编写一个嵌套的 if 语句来启用这种情况:

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
    print(" at least 2 years and you must have good or"
    print(" excellent credit to be considered for a loan.")
  }
}
else {
  print("Sorry, you must make at least $25,000 to be ")
  print(" considered for a loan.")
}
```

下面是该程序的几次运行，测试了每一种可能的场景:

```
Enter your salary: 25001
Enter your length of employment at current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Good
Sorry, you must be employed at your current job for at least 2 years
and you must have good or excellent credit to be considered
for a loan.Enter your salary: 25001
Enter your length of employment at current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Good
You can be considered for a loan.Enter your salary: 25001
Enter your length of employment at current job: 2
What is your credit (Poor, Fair, Good, Excellent)? Fair
Sorry, you must be employed at your current job for at least 2 years
and you must have good or excellent credit to be considered
for a loan.Enter your salary: 24999
Sorry, you must make at least $25,000 to be considered for a loan.
```

# 转换语句

使用`if`语句来实现*从备选方案中选择*模板的替代方案是`switch`语句。`switch`语句是一种更有条理的语句，当程序需要选择的选项表示为单个值而不是范围时，该语句运行良好。

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

一个例子将有助于澄清`switch`语句是如何工作的。质量分数用于计算学生的平均分数(GPA)。A 值 4 个质量点，B 值 3 个质量点，C 值 2 个质量点，D 值 1 个质量点，F 值 0 个质量点。以下程序要求用户输入课程的字母等级，然后确定质量分数:

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

以下是该程序几次运行的结果:

```
What is the letter grade for the course? B
A grade of B is worth 3 quality points.What is the letter grade for the course? C
A grade of C is worth 2 quality points.What is the letter grade for the course? A
A grade of A is worth 4 quality points.
```

`switch`语句的另一个流行用法是实现一个菜单。以下程序演示了用于执行简单计算的菜单系统。以下是程序:

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

以下是该程序的几个运行示例:

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

我已经向您展示了实现 Select From Alternatives 程序模板的两种方法——if 语句和 switch 语句。稍后，当我谈到数组数据结构时，我将向您展示如何使用一种叫做表查找的东西来实现这个模板。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*