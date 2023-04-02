# 4 个让 JavaScript 开发者在未来遭受痛苦的奇怪错误

> 原文：<https://javascript.plainenglish.io/4-mistakes-that-make-javascript-developers-suffer-in-future-eaf1314b3e09?source=collection_archive---------6----------------------->

## 每个 JavaScript 开发人员都应该知道的残酷事实

![](img/df749e820635446348357b8098e9656c.png)

Photo by fauxels from [Pexels](https://www.pexels.com/photo/selective-focus-photo-of-man-closing-his-eyes-3228845/)

没有一个开发人员喜欢犯错误。

每个开发人员都希望他们的代码是完美的。我们，开发人员，希望我们的代码不仅没有错误，而且是可读的。

但是我们犯的某个错误会让我们在未来遭受痛苦。当我们犯这些错误时，我们对它将造成的困难一无所知。然而，我们一次又一次地犯这些错误。

以下是其中的四个错误。

# 1.使用易混淆的长名称

短名称在使用时不能提供足够的信息。这就是为什么我们避免写短函数和变量名。

当短名称不能提供足够的上下文时，大多数程序员会开始使用长的描述性名称。

描述性的名字是好的，但是又长又混乱的描述性名字是不好的。描述性名称和令人困惑的长描述性名称之间的界限很微妙。

当你写的名字传达了太多的意思。它会让代码读者感到困惑。

如果您将函数名写成这样:

```
vectorControl.addAndDisplayModifiedAndCopiedScalers();
```

变得难以理解。

看了上面的函数名，任何一个程序员都会在两件事之间感到困惑:

*   如果上述函数添加并显示既被修改又被复制的定标器。
*   上述函数添加并显示修改的定标器和复制的定标器。

一个刚刚开始学习编码的初学者不仅会感到困惑，还会害怕冗长的描述性函数名。

## 如何将一个长名字拆分成多个部分

我们将使用上述函数发生的不同事情来将名称分成几个部分。

如果您想对上述功能进行更改。只要确保新函数一次只做一件事。

您可以将上述功能分为四个独立的功能:

```
vectorControl.addCopiedScalers();vectorControl.displayModifiedScalers();vectorControl.addModifiedScalers();vectorControl.displayCopiedScalers();
```

不要用长名字来掩盖你糟糕的抽象。

长名字不是问题，通常是混乱的抽象造成了混乱。

[](https://sanjay-priyadarshi.medium.com/meet-a-programmer-who-turned-an-open-source-platform-into-a-7-500-000-000-company-645e14c53c8) [## 遇到一个程序员，他将一个开源平台变成了一家价值 75 亿美元的公司

### 激励年轻程序员的旅程

sanjay-priyadarshi.medium.com](https://sanjay-priyadarshi.medium.com/meet-a-programmer-who-turned-an-open-source-platform-into-a-7-500-000-000-company-645e14c53c8) 

# 2.代码注释违反了干燥原则

“不要重复自己。”

如果你是一名开发人员，你每天至少会听到一次以上的术语。

资深开发人员不断向初级开发人员重复这个原则。

大多数程序员认为，只有当您在代码库中的两个或更多地方编写相同的代码时，才会发生干违反。

Dry 违例可能出现在代码库中的多个点上。

如果任何开发人员已经编写了自我文档化的代码，并且还在那里编写了注释来解释这些代码。

在那种情况下，干燥原则被违反了。

为了在代码中做一个小的改变，我们必须在代码和注释中做一些改变。

意味着知识被复制了。

这里有几个例子:

```
return 1;       //returns 1getUserInfo();  //This function helps to get user information.i--;            //decrease the value of i by 1
```

如果你的注释没有给代码增加意义，就不要写注释。

# 3.不写小函数

任何一个以写代码为生的开发者都会阅读大量的代码。

作为开发人员，我们日常生活的 95%都涉及到阅读他人的代码。

我们在以下情况下阅读代码:

*   我们正在寻找修复代码错误的方法。
*   我们正在阅读文档。
*   我们学习一种新的语言或框架。

我们总是在阅读某人的代码。

作为开发人员，我们已经读取了具有以下功能的函数:

*   500 多行代码。
*   超过 200 行代码。
*   不到 100 行代码。
*   不到 50 行代码。

理想情况下，所有开发人员都希望函数的长度在 50-100 行可读代码的范围内。

如果一个函数包含超过 200 行代码。我们不想读它，因为它很难理解。

对于较老的语言，保持函数的长度很小几乎是不可能的。

使用现代语言，您可以保持函数的长度较小。使用较少代码行读取函数的开发人员必须进行较少的上下文切换。

这里有一个小例子:

```
function payEmployees(employees){
    employees.forEach(employee => {
        const employeeRecord  = database.lookup(employee);
        if(employeeRecord.isActive()) {
            pay(employee);
        }
    });
}
```

上述功能可以分为两个独立的功能。

```
function payActiveEmployees(employees){
    employees.filter(isActiveEmployee).forEach(pay);
}function isActiveEmployee(employee){
    const employeeRecord = database.lookup(employee);
    return employeeRecord.isActive();
}
```

上面两个小函数就变得易读了。

当有可能将一个功能拆分成单独的功能时，就这么做。

函数长度尽量小，因为小函数对程序员的帮助很大。

[](https://sanjay-priyadarshi.medium.com/a-19-year-old-programmer-dropped-out-of-college-to-build-a-2-300-000-000-company-in-2-years-1055963ec1db) [## 一名 19 岁的程序员从大学辍学，在两年内创建了一家价值 23 亿美元的公司

### 没有人能预料到他的成功

sanjay-priyadarshi.medium.com](https://sanjay-priyadarshi.medium.com/a-19-year-old-programmer-dropped-out-of-college-to-build-a-2-300-000-000-company-in-2-years-1055963ec1db) 

# 4.不要在情感上脱离他们的代码

在情感上远离你的代码和设计是一种超能力。

如果您过去编写过不再适用的代码，您应该删除这些代码。

当你把你的代码当成自己的孩子时，它会迫使你把对代码的批评当成是针对你个人的。

当你远离你的代码时，你会积极地接受对你代码的反馈，而不是感觉被攻击。

如果评审员要求你删除一段代码并重写，保持超然可以防止你与评审员争论。

如果你保持超然，你会平静地看待你的代码。

如果经过仔细的调查，你发现你犯了错误，你更有可能改变它，即使代码花了一个月的时间来编写。

# 摘要

1.  应该避免长名字。
2.  代码注释可能违反 DRY 原则。
3.  不要写小函数。
4.  你不是你的代码。

[](/a-programmer-turned-entrepreneur-built-a-27-700-000-000-app-using-insights-from-a-failed-game-df017835939) [## 一名程序员从一个失败的游戏中吸取经验，开发了一个价值 277 亿美元的应用程序

### 详细了解此人的生活

javascript.plainenglish.io](/a-programmer-turned-entrepreneur-built-a-27-700-000-000-app-using-insights-from-a-failed-game-df017835939) [](/two-programmers-turned-7-lines-of-code-solution-into-95-000-000-000-empire-961f200b3082) [## 两位程序员将 7 行代码的解决方案变成了 950 亿美元的帝国

### 这是一次我非常希望所有年轻程序员都能读到的旅程。

javascript.plainenglish.io](/two-programmers-turned-7-lines-of-code-solution-into-95-000-000-000-empire-961f200b3082) 

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

你可以在这里加入。

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***