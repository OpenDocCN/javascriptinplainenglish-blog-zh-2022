# 理解面向对象的类型脚本的一篇文章

> 原文：<https://javascript.plainenglish.io/one-article-to-understand-typescript-object-oriented-59346983c466?source=collection_archive---------7----------------------->

## 理解静态属性、静态方法、多态、抽象类和接口定义，并举例说明。

![](img/d6bd20378c6b3e2743ce2942f9120287.png)

在上一篇文章中，我们介绍了 TypeScript 中函数、类和继承的定义。

在本文中，我们继续用一些简单易懂的例子来介绍静态属性、静态方法、多态、抽象类和 TypeScript 中的接口的定义。

## 1.静态属性和静态方法。

`static` 关键字用于修改 TypeScript 中的静态属性和静态方法。静态属性和静态方法无需实例化即可访问，访问时可以直接通过类名调用。

## 2.TypeScript 中的多态性。

多态意味着为父类定义一个方法，子类继承了它之后，可以重写这个方法，以符合子类自己的要求。

## 3.抽象类和抽象方法。

## 界面的定义

在面向对象编程中，接口是规范的定义，它定义了规范的行为和动作，在编程中，接口起着限制和规范的作用，接口定义了某一组需要遵守规范的类，接口不关心这些类的内部状态数据，也不关心这些类中方法的实现细节，它只规定这组类必须提供某些方法，提供这些类的方法才能满足实际需要。

接口中的 TypeScript 类似于 Java，但也增加了更灵活的接口类型，包括属性、函数、可索引和类。

1.  **在 TypeScript 中定义属性接口。**

还可以定义接口中的属性是否可选。

使用属性接口约束实现 Ajax 请求。

**2。在 TypeScript 中定义函数类型接口。对传递给方法的参数的约束，以及返回值。**

**3。在 TypeScript 中定义可索引类型接口。在数组和对象上实现约束。**

也可以在较少使用的对象上实现约束。

**4。用于在 TypeScript 中定义类类型的接口。实现对类的约束。**

**5。TypeScript 中接口的扩展。接口继承的实现。**

接口也可以在实现接口约束的同时实现类继承。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***