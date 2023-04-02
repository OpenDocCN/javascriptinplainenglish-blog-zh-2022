# 有经验的开发人员使用的 5 种基本但强大的重构技术

> 原文：<https://javascript.plainenglish.io/5-basic-but-powerful-refactoring-techniques-used-by-experienced-developers-c1b9a879db78?source=collection_archive---------5----------------------->

## 保持代码库整洁的简单方法

![](img/323bf890781a5bb45f7612ea8d5a2fd8.png)

Photo by [kelisa Bernard](https://unsplash.com/@kellisa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

重构是关于保持你的代码库干净。

但是大多数文章和书籍都给出了冗长的例子，使问题变得复杂。

在这里，我用简单的例子介绍了五种基本的重构技术。

# 1.删除无用的变量

看一下这个例子:

```
const person= { firstName:"Rock", lastName:"Doe", age:50, eyeColor:"brown",};let str = person.lastName;if(str === "Doe"){ console.log(true);
}
else{ console.log(false);}//result: true
```

在上面的例子中，我们不需要`str`变量。

如果没有`str`变量，我们可以很容易地工作。

你可以这样做:

```
const person= { firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};if(person.lastName === "Doe"){ console.log(true)
}else{ console.log(false)
}//result: true
```

有时名字不仅仅是一种表达。

# 2.有意义的函数参数名

看看这个函数:

```
function calculateArea(a,b){ //do what you want}
```

函数名在任何代码库中都扮演着重要的角色。

每本关于干净代码的书都提到你的函数名应该有意义。我不想重复了。

就像函数名一样，参数名在您以后尝试重构代码时也起着重要的作用。

如果你把上面的函数写成这样就更好了:

```
function calcuateArea(length, breadth){ //do what you want}
```

# 3.如果多次使用，重命名变量

为变量编写清晰的名称对于代码库的可读性非常重要。

如果你写了一个好的变量名，它会变得不言自明。

如果你要在一个代码库中使用一个变量。最好给它取一个单字母的名字。

但是如果一个变量被多次使用，你必须给它一个有意义的名字，这样它就可以不言自明了。

这里有一个这样的例子:

```
let xyz = length * breadth;
```

在上面的例子中，变量`xyz`没有传达正确的信息。你必须写出有意义的变量名。

这就是你重写上述变量的方法。

```
let area = length * breadth;
```

# 4.用查询替换临时

稍后将在代码中使用的局部变量可以移到单独的方法中。

以下面的函数为例:

```
function compareArea(){ let calculatedArea = length * breadth; if(calculatedArea > 100){ return calculatedArea - 5; } else { return calcualtedArea + 5; }}
```

您需要将整个表达式移动到一个单独的方法中，并返回结果。

像这样做:

```
function compareArea(){ if(calculateArea() > 100){ return calculateArea() - 5; } else{ return calculateArea() + 5; }}function calculateArea(){ return length * breadth}
```

## 以下是一些好处:

*   有时同一个表达式被用在多个函数中。这将帮助你一遍又一遍地使用这个表达。
*   将会有更少的代码重复。
*   提高代码可读性。

## 一个缺点

这种重构技术会导致一些性能问题。

# 5.如果可能，拆分临时变量

从长远来看，使用相同的变量名存储一些中间值可能会产生问题。

这里有一个这样的例子:

```
let radius = 5;let temp = 3.14 * radius * radiusconsole.log(temp);let temp = 2 * 3.14 * radiusconsole.log(temp);//result: Identifier 'temp' has already been declared
```

作为程序员，我们每个人都有使用同一个变量存储中间值的习惯。

我们主要使用`temp`变量。

但是如果我们在包含数千行代码的代码库中使用同一个变量。它会在将来产生问题。

有时这会制造噩梦。

像这样做:

```
let radius = 5;let area = 3.14 * radius * radiusconsole.log(area);let perimeter = 2 * 3.14 * radiusconsole.log(perimeter);//result: 78.5
          31.400000000000002
```

## 这是拆分的一些好处

*   如果你拆分了临时变量，你的代码将很容易维护。您可以轻松替换任何变量，而不用担心任何不必要的影响。
*   一旦使用了这种技术来重构代码，就可以很容易地从现有方法中提取方法。

# 摘要

1.  删除不必要的变量。
2.  编写有意义的函数参数名。
3.  如果可能，请更改变量名。
4.  尝试用 query 替换 Temp。
5.  溢出临时变量。

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

你可以在这里加入。

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****