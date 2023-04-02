# 实现 JavaScript Extends 关键字的 6 种方法

> 原文：<https://javascript.plainenglish.io/6-ways-to-implement-the-javascript-extends-7fa1fc6a6b3e?source=collection_archive---------1----------------------->

## 轻松实现 JavaScript extends 关键字的 6 种方法。

![](img/ba20186a609f459832b0e8ad575f0970.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种奇怪的语言。一个需求可以通过多种方式实现(免费！)，这真的很神奇！

本文将帮助您学习如何用 6 种方式在 JavaScript 中实现扩展的概念

## 1.原型链延伸

构造函数、原型和实例的关系:每个构造函数都有一个原型对象，原型对象包含一个指向构造函数的指针，实例包含一个指向原型对象的指针。

继承的本质是复制，即重写原型对象，用新类型的实例替换。

Prototype Chain Extends

## 不足之处

多个实例对引用类型的操作可能被篡改。

# 2.借用构造函数扩展

使用父类的构造函数来增强子类实例，相当于将父类的实例复制到子类中(不使用原型)

Borrowing Constructor Extends

核心代码是 `Parent.call(this)`，父构造函数在创建子类实例时被调用，所以 Child 的每个实例都会复制 Parent 中的属性。

## 不足之处

*   只能继承父类的实例属性和方法，不能继承原型属性/方法
*   无法实现重用，每个子类都有一个父类实例函数的副本，这会影响性能

# 3.原型扩展

实现原理是用一个空对象作为中介，直接把一个对象赋给空对象构造器的原型。

Core

`func()`函数执行传入对象的浅层复制，将**构造函数 F 的原型指向传入对象**。

Prototypal Extends

## 不足之处

*   原型链继承了指向同一的多个实例的引用类型属性，存在被篡改的可能。
*   无法传递参数。

另外， `Object.create()`方法存在于 ES5 中，可以代替上面的`func method.`

# 4.寄生延伸

核心实现原理:在原型继承的基础上，增强对象并返回构造函数

Parasitic Extends

这个函数的主要功能是在构造函数中添加属性和方法来增强函数

**缺点:与原型继承相同**

# 5.寄生成分扩展

通过借用的构造函数传递参数和寄生模式的组合来实现扩展

Parasitic Compositional Extends

这个例子的效率在于它只调用了一次`SuperType` 构造函数，因此避免了在`SubType.prototype`上创建不必要的、多余的属性。

同时，原型链保持不变；因此，`instanceof` 和`isPrototypeOf()`可以正常使用

顺便说一下，**这是最成熟的方法，也是现在库实现的方法**

# 6.ES6 类继承扩展

[extends 关键字](https://developer.mozilla.org/en-US/docs/Glossary/Class)主要用于类声明或类表达式中，以创建一个类，该类是另一个类的子类。

其中，`constructor` 代表建造者。一个类中只能有一个构造函数。如果超过一个，将报告`SyntaxError` 。如果没有显式指定构造函数，将添加默认的`constructor` 方法。使用示例如下

Final Version

# 总结

1.  函数声明和类声明的区别。
    函数声明被提升，而类声明没有。首先，您需要声明您的类，然后访问它，否则，代码将抛出一个 ReferenceError
2.  ES5 扩展和 ES6 扩展的区别

*   ES5 中的扩展本质上是先创建子类的一个实例对象，然后将超类的方法添加到 this (Parent.call(this))。
*   ES6 的扩展是不同的。本质上，首先创建父类的实例对象 this，然后使用子类的构造函数来修改 this。因为子类没有自己的 this 对象，所以必须先调用`superclass` 的`super() method`，否则新实例会报错。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***