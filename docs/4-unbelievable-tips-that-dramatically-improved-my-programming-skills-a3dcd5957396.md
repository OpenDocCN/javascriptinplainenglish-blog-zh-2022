# 4 个令人难以置信的技巧极大地提高了我的编程技能

> 原文：<https://javascript.plainenglish.io/4-unbelievable-tips-that-dramatically-improved-my-programming-skills-a3dcd5957396?source=collection_archive---------8----------------------->

## 对我帮助很大的几条建议

![](img/18fb61a3bc32abbe97728aa13328519d.png)

Photo by [Andrea Piacquadio](https://www.pexels.com/photo/man-in-blue-dress-shirt-standing-beside-tree-trunks-3764180/) from Pexels

在一个理想的世界里，每个程序员都有很好的编程技能。分配给任何程序员的工作都需要相同的天数。

实际上，不同的程序员有不同的编程技能水平。

完成同样的工作，一个程序员可能需要五天，另一个可能需要十天。这取决于一个程序员的技能。

有了正确的提示和技巧，任何程序员的编程技能都可以得到提高。在这里，我提到了其中的四个技巧。

# 1.如果可能，内联函数

当函数体比函数本身更明显时。您必须内联函数。

## 让我们通过一个例子来看这个问题:

```
function aFunction(number){ let str = checkIsEven(number);

    return str;}function checkIsEven(number) { return number.isEven;}
```

这是调试上述代码的方法。

```
function aFunction(number){ let str = number.isEven; return str;
}
```

## 为什么需要内联函数

当您阅读代码时，有时您会发现一些函数只是将工作委托给另一个函数。

很多时候这种委托是有用的，但是当功能的数量不必要地增加时。取代它而不是希望通过不同的功能是有意义的。

一旦从代码中删除了不必要的函数，整个代码库就会变得简单明了。

# 2.避免写短名字

以一个作家为例。

如果编剧的观众觉得故事很混乱，不理解。他们会很沮丧。最终，观众会不再关注这个故事。

作家必须确保观众对这个故事着迷。

当开发人员编写任何代码时，他们的代码都有受众。可能受众少，但是他们的代码是有受众的。

一个不考虑受众的程序员可能会认为写下面这个函数没问题:

```
function couEmp(id, r){ for(let z = 0; z < emp.length(); z++){ if (emp[z].id === id && r(emp[z])){ emp[x].t++; }
    }
}
```

上述函数的目的是增加在`emp`数组中可用的特定对象的`t`属性的值。

当你阅读上面的代码时，你只会在基本层面上理解代码作者在做什么。

您将无法理解编写该函数背后的目的。由于所使用的简称，你不会理解它存在背后的原因。

当有人第一次读到它时，他们不得不猜测这些名字的用途。

## 如何更好地编写上面的函数

```
function countEmployeeByIdIfRequired(id, requirement){

    for(let i = 0; i < employees.length; i++){ let employee = employees[i]; if (employee.id === id && requirement(employee)){ employee.tTotal++; }
    }
}
```

如果你用更有意义的名字编写函数，编写函数背后的思想就变得清晰了。

上述函数的目的是查找具有满足特定要求的特定 ID 的雇员。一旦找到这样的雇员,`tTotal`值就增加 1。

有了新名字，我们可以得出结论，雇员可以在雇员数组中出现任意多次。通过增加`tTotal`的值，在`id`的帮助下跟踪员工的次数。

仅仅通过输入几个有意义的名字，我们就可以得出很多结论。这就是写有意义名字的力量。

# 3.简单的代码是美丽的代码

大多数程序员花了数百个小时来确保他们的代码易于阅读和维护。

他们优化速度，努力保持代码整洁。

即使在优化了这么多因素之后，他们最终还是过度设计了他们的代码。

如果每个程序员都想写出不凌乱的代码。

为什么会这样呢？即使优化了这么多东西，大多数程序员最终还是会写出混乱的代码。

这是因为作为程序员，我们有时会迷失在所有这些原则中，比如不要重复自己(DRY)，单一责任原则(SRP)，开放和封闭原则(OCP)，以及保持代码整洁。

如果我们程序员专注于一个简单的因素，而不是迷失在这些原则中，我们将写出漂亮的代码。

简单的代码是美丽的代码。这是毫无疑问的。

没有简单的代码定义。对你来说简单的事情对其他人来说可能很难。

要解决这个问题，你需要阅读其他优秀开发者写的代码。

你应该阅读好的开源项目中编写的代码，并根据他们的说法，找出什么是简单的代码。一旦你开始阅读其他开发者的代码，你就会让你的定义变得‘简单’。

一旦你有了简单的定义，当你写代码时，你应该坚持这个定义。相信我，这将是干净的和可读的。

# 4.尽可能使用函数式编程

99.9%的编程课程只关注面向对象编程。

面向对象编程使得整个代码库看起来很复杂。

开发人员没有解决现实世界的问题，而是一直在思考所有那些“设计模式”和“抽象”

OOP 对于整个编程生态系统来说是一个巨大的失败。

函数式编程是面向对象编程的一个很好的替代品。

当你只借助函数来编写一个完整的程序时，就叫做函数式编程。

有了函数式编程，并发性就变得安全了，测试代码变得容易了，调试变得有趣了。

你不会像以前调试 OOP 代码时那样迷路了。

让我们通过一个例子来看看使用函数式编程的一点好处。

## 这就是函数不纯的缺点

取下面的函数:

```
let abc = 0function addNumber(aNumber){
    abc = abc + aNumber;
    return abc;
}
```

上面，addNumber()在多次调用时不会给出相同的结果。

```
addNumber(3);
console.log(addNumber(3));
```

我已经调用了 addNumber()两次。产生的输出将是:

```
//This is the output
6
```

如果您再次调用 addNumber()，将会改变输出。

```
addNumber(3);
addNumber(3);
console.log(addNumber(3));
```

输出将是:

```
//Here is the output
9
```

可以调用上面的 addNumber()作为不纯函数。

上述函数可以改变其作用域之外的变量。即使输入保持不变，每次调用 addNumber()时，输出仍然会发生变化。

## 这是纯函数的优点

纯函数的工作方式与数学函数相同。

纯函数可以像数学函数一样进行计算。

纯函数的一个例子:

```
function pureAdd(aNumber1, aNumber2){ return aNumber1 + aNumber2;
}
```

上面的 pureAdd()永远不会根据它被调用的次数来改变它的结果。

你可以任意多次调用一个纯函数，它都会给出相同的结果。

让我们调用上面的函数四次。

```
pureAdd(0,3);
pureAdd(0,3);
pureAdd(0,3);
console.log(pureAdd(0,3));
```

输出保持不变。

```
// This is the output
3
```

纯函数是确定性函数。

与命令式编程相比，使用函数式编程还有其他一些好处。

# 摘要

1.  尽可能使用内联函数。
2.  写代码时不要写短名字。
3.  简单的代码是美丽的代码。
4.  使用函数式编程。

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

你可以在这里加入。

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****