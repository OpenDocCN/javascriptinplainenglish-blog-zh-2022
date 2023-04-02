# 用 JavaScript 调用和应用

> 原文：<https://javascript.plainenglish.io/call-and-apply-in-javascript-f4974fc781aa?source=collection_archive---------11----------------------->

## JavaScript 中的调用和应用简介

![](img/de6bb3174ea6756508b36e943136f77c.png)

## 介绍

当我们使用调用和应用时，我们通常是在处理对象。通过使用这些方法，我们可以从一个对象到另一个对象继承对象方法。例如，如果一个方法是在对象一上定义的，它可以被对象二调用。

虽然 call 和 apply 背后的概念是相似的，但要注意的重要区别是，当您使用 call 时，您显式地传递参数，而使用 apply 时，您将第二个参数作为数组传递。让我们看一个例子来阐明这一点。我们将从查看调用方法开始。

## 打电话

```
const person = {
  details: function() {
    return `My name is ${this.name}`
  }
}const bob = {
  name: "Bob"
}console.log(person.details.call(bob));
//Returns ---> My name is Bob
```

在上面的例子中，我们创建了一个*人*对象。在对象内部，我们创建一个名为*细节*的方法。这个方法返回一个带有人名的模板文本。接下来，我们创建另一个名为*鲍勃*，*鲍勃*有一个*名称*属性和值集。最后，在控制台日志中，我们返回使用 *call()* 方法调用 *details* 方法的结果，并传入 *bob* 作为参数。如果我们在这里不使用 call 方法，我们将得到下面的结果。

```
console.log(person.details)
'My name is undefined'
```

因此，通过使用 call，我们可以使用在 *person* 对象上定义的 *details* 方法，但是在我们单独的 bob 对象上。这个指的是你作为参数传递给调用的内容。如果我们在控制台记录*细节*方法中*这个*的值，我们就可以确定这一点。

```
const person = {
  details: function() {
    console.log(this)
    //returns ---> {name: 'Bob'} return `My name is ${this.name}`
  }
}const bob = {
  name: "Bob"
}console.log(person.details.call(bob));
//Returns ---> My name is Bob
```

## 应用

Apply 与 call 非常相似，只是我们必须传递一个数组作为第二个参数。让我们首先向使用 call 的初始示例添加一个参数。

```
const person = {
  details: function(age) {
    return `My name is ${this.name} and I am ${age} years old.`
  }
}const bob = {
  name: "Bob"
}console.log(person.details.call(bob, 12));
//Returns ---> My name is Bob and I am 12 years old.
```

在上面的例子中，我们现在在模板文字中使用的*细节*方法中为*年龄*设置一个参数。当我们使用 call 方法时，我们在传入 *bob* 对象之后，再传入这个参数的值。如果我们使用 apply，我们需要在这里使用一个数组。如下例所示。

```
const person = {
  details: function(age) {
    return `My name is ${this.name} and I am ${age} years old.`
  }
}const bob = {
  name: "Bob"
}console.log(person.details.apply(bob, [12]));
//Returns ---> My name is Bob and I am 12 years old.
```

如果我们在使用 apply 时没有传入数组，我们会得到下面的错误。

```
Uncaught TypeError: CreateListFromArrayLike called on non-object
    at <anonymous>:9:28
```

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****