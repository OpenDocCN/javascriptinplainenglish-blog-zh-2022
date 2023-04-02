# JavaScript 中的 instanceof 运算符是什么

> 原文：<https://javascript.plainenglish.io/what-is-the-instanceof-operator-in-javascript-2f74e88a2a4d?source=collection_archive---------10----------------------->

## 了解如何在 JavaScript 中使用 instanceof 运算符

![](img/a09bb99c91a1a71460d0bdf81692f93a.png)

## 介绍

在 JavaScript 中 *instanceof* 是一个操作符。运算符要么用于计算，要么用于逻辑。操作符的*实例将查看一个操作数(我们执行操作的对象)是否是我们传递的值的实例。当我们使用 instance of 时，我们将操作数放在左边，而将传递的值放在右边。如下例所示*

```
someoperand instanceof somevalue
```

## 例子

当我们使用操作符的*实例时，它将检查操作数是否是我们传递的值的实例，它还将检查值的原型链。返回值将总是布尔值(真或假)。让我们先看一些基本的例子。*

```
const pets = {
  amount: 4
};pets instanceof String
//Returns ---> falsepets instanceof Number
//Returns ---> falsepets instanceof Object
//Returns ---> true
```

在上面的例子中，我们创建了一个存储在名为 *pets* 的变量中的对象文字。在 *pets* 对象内部，我们创建了一个名为 *amount* 的属性，值为 4。接下来我们使用 *instanceof* 操作符来检查 pets 是否是字符串、数字和对象的实例。String 和 Number 都返回 false。尽管存储在 *pets* 中的值是一个数字，但我们检查的是对象本身，而不是对象内部的属性。因为 pets 是一个对象，当我们继续检查 pets 是否是对象的实例时，我们得到 true。

让我们看另一个例子。

```
const greeting = "Hello"greeting instanceof String//Returns false
```

在上面的例子中，我们声明了一个名为 *greeting* 的变量，并将字符串 *Hello* 赋给这个变量。接下来我们检查*问候*是否是字符串的一个实例。我们会犯错。这可能会让你大吃一惊。当我们使用操作符的*实例时，我们检查它是否是字符串对象的实例，而不是检查类型。当我们创建 *greeting* 变量时，我们使用了一个字符串文字，所以它实际上不是 string 的一个实例。如果我们想让它返回 true，我们需要做以下事情。*

```
const greeting = new String("Hello")
greeting instanceof String//Returns ---> true
```

当你使用类并且你想检查某个东西是否是一个类的对象时，操作符的实例会很有用。让我们来看一个例子。

```
class Car {}
const honda = new Car()honda instanceof Car
//Returns ---> true
```

我将用最后一个例子来结束这篇文章。

```
const arr = [1, 2, 3]arr instanceof Array
//Returns ---> truearr instanceof Object
//Returns ---> true
```

在上面的例子中，我声明了一个名为 *arr* 的变量，并给它分配了一个包含一些值的数组。接下来使用操作符的*实例，我检查*数组*是否是*数组的*实例。所以我真的回来了。接下来，我检查它是否是 Object 的实例。我也得到真实的回报。您可以期待函数以类似的方式工作。原因是它们继承自原型链中的 Object。*

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **