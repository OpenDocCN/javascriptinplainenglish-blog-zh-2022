# JavaScript 点符号与括号符号:在什么情况下使用哪个

> 原文：<https://javascript.plainenglish.io/javascript-dot-notation-vs-bracket-notation-which-to-use-when-e24117e44d71?source=collection_archive---------2----------------------->

## 点符号和括号符号的区别，以及何时应该使用它们。

![](img/abe082df67ea2c7dbd56272f507bacf1.png)

Photo by [franco alva](https://unsplash.com/@franquito4133?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当学习一门新的编程语言时，首先要学习的事情之一是如何访问数组和对象中的元素。在 JavaScript 中，有两种方法可以做到这一点:点符号和括号符号。在这篇博文中，我们将讨论这两种符号之间的区别，以及何时应该使用这两种符号。

## 点符号

点符号是 JavaScript 中访问元素最常见的方式。要使用点标记法，您只需简单地写下对象的名称，后跟一个点和您想要访问的属性的名称。例如，如果我们有一个名为“person”的对象，它有一个名为“name”的属性，我们可以使用`person.name`来访问 name 属性。

## 括号符号

括号符号没有点符号常见，但在某些情况下很有用。要使用括号表示法，您可以写下对象的名称，后跟括号和要访问的属性。例如，如果我们有一个名为“person”的对象，它有一个名为“name”的属性，我们可以使用`person[“name”]`来访问 name 属性。

## 主要差异

现在我们已经看到了点符号和括号符号是如何工作的，让我们讨论一下这两种符号之间的主要区别。

点符号比括号符号书写更快，更容易阅读。

但是，变量可以用括号表示，但不能用点表示。当您想要访问某个属性，但事先不知道该属性的名称时，这尤其有用。例如，如果我们想遍历一个对象中的所有键，并访问它们的值，我们可以使用括号符号。

```
for (let key in obj) { console.log(obj[key]);}
```

括号符号允许您访问名称中带有特殊字符的属性，而点符号则不能。

```
let obj = {“foo.Bar”: 2}obj[“foo.Bar”] // valid syntaxobj.foo.Bar //invalid syntax
```

总之，点符号是 JavaScript 中访问元素最常见的方式。但是，在某些情况下，括号符号更合适。当您想要使用变量来访问属性时，或者如果属性的名称中有特殊字符，您应该使用括号表示法。

我希望这篇文章能消除你的任何困惑。祝你的编码面试好运！

*更多内容看*[**o**](https://plainenglish.io/)**。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**