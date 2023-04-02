# 值得了解的 5 个 JavaScript 概念，简单解释一下

> 原文：<https://javascript.plainenglish.io/5-javascript-concepts-worth-knowing-explained-briefly-df3d6b5861c9?source=collection_archive---------9----------------------->

![](img/67f360d3c2520f873085694beff4741a.png)

我之前分享过十个 JavaScript 概念。在这篇文章中，我将讨论五个更容易理解的概念。

## **1。首先，我们来看看四个运算符是什么**

先说分类，分为两类:

1.附加类别:

只要有带字符串的操作，都会转换成字符串。如果它不是一个字符串(和一个数字)，那么把它转换成(一个字符串)或一个数字。

那么如何判断先转换成数字还是先转换成字符串呢？这涉及到触发三种类型转换的加法运算。参见“比较运算符”，至“基本方法”。

2.非添加剂类:

只要其中一个是数字，另一个就转换成数字。

## **2。先来了解一下什么是文案**

任何语言都有自己的深抄和浅抄。深拷贝有利于数据的完全独立，但如果都是深拷贝，内存就不会继续上升，于是就有了浅拷贝。

1.浅拷贝通常是指拷贝第一层或内部的数据，更深一层的数据仍然指向同一个地址，原对象在被修改时也会受到影响。

**注:**基于内存节省，我们日常使用的很多函数都是浅拷贝，比如我们的 spread 运算符，还有 Object.assign、contact、slice 等。

2.深度复制完全复制一个新对象，原始对象不再受任何修改的影响

描述:

1.可以使用 JSON.parse(JSON.stringify(obj))。最快的性能。它的缺点也很明显。首先，函数、未定义、符号等值是无法复制的。如果第二个对象有自己的循环调用，将会报告一个错误。

2.使用递归在每一层重新创建对象并赋值

3.如何使用 jQuery，可以考虑，$。extend( [deep ]，target，object1 [，objectN ])，也是深度复制的一种。

4.还可以使用 lodash.js，cloneDeep 方法进行深度复制。

## **3。调用函数的几种方法**

在 JavaScript 中，有四种方法可以调用函数:

1.方法调用模式(指向自身)

2.函数调用模式(这指向 windows)

3.构造函数调用方式(使用原型构造，JS 放弃这种方式)

```
function myFunction(arg1, arg2) {
    this.firstName = arg1;
    this.lastName  = arg2;
}

// This creates a new object
var x = new myFunction("Bob","Doe");
x.firstName;
```

4.应用调用模式(使用应用更改此对象)

```
function myFunction(a, b) {
    return a * b;
}
myArray = [1,2];
myFunction.apply(myObject, myArray);
```

函数调用，由自身携带，记得要有**这个**和参数

## **4。高阶函数的简单理解**

以函数为参数或返回函数的函数可以是高阶函数。所以常见的方法有:映射、过滤、绑定、应用等。当然，你还是要明白高阶函数实现 AOP。

## **5。Currying 功能**

Currying，从实现上来说，就是返回一个高阶函数，通过闭包保存传入的参数。当传入参数数量不足时，递归调用 bind 方法；当数量足够时，立即执行该功能。

Currying 是一种将接受多个参数的函数转换成一系列接受一个参数的函数的技术。

curried 函数是一个逐步传递参数的函数。可以事先传递参数，不让他执行内容，而是在参数满足时调用函数。感情可以用来做一些未知的判断。

**好了，这次分享到此结束。下一次，我将继续分享剩下的 5 个 JavaScript 概念。欢迎大家一起讨论。**

**感谢您的阅读，期待您的关注。**

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*