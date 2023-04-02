# 重新学习前端——面向 JavaScript 对象

> 原文：<https://javascript.plainenglish.io/relearning-the-front-end-javascript-object-oriented-913077e735bf?source=collection_archive---------0----------------------->

![](img/4569366773dedd624b0d104542dbaf8f.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我会花一个月的时间整理前端相关的知识。一方面我会巩固自己的技能。另一方面，我会用它来分享初级前端工程师的学习路径和高级前端工程师的知识复习。

总体文章目录

*   [重新学习前端— HTML](/relearn-the-front-end-html-26a38c5ba196)
*   [重新学习前端——CSS](/relearn-the-front-end-css-4d74eb5981f8)
*   [重新学习前端— JavaScript 基础知识](/relearn-the-front-end-javascript-basics-d770eefd791f)
*   [重新学习前端——面向 JavaScript 对象](/relearning-the-front-end-javascript-object-oriented-913077e735bf)
*   [重新学习前端— JavaScript V8 引擎机制](/relearning-the-front-end-javascript-v8-engine-mechanism-cc6457b43aff)
*   [重新学习前端—浏览器渲染机制](/relearning-the-front-end-browser-rendering-mechanism-efbfc19d225f)
*   [重新学习前端—浏览器缓存策略](/relearn-the-front-end-browser-caching-strategy-21cd081886d)
*   [重新学习前端—排序算法](/relearn-the-front-end-sorting-algorithm-348f939632e0)
*   [重新学习前端—设计模式](/relearning-the-front-end-design-patterns-e95444b6bdb)
*   [重新学习前端网络](/relearn-the-front-end-network-b0402a870336)
*   [重新学习前端—前端安全](/relearning-the-front-end-front-end-security-bbc20ded6b12)

这篇文章是关于 JavaScript 面向对象的。

JS 中的一切都是对象，但 JS 不是真正的面向对象( **OOP** )语言，因为它缺少类的概念。虽然 ES6 引入了类和扩展，但是我们可以很容易地实现类和继承。但是 JS 没有真正的类。JS 类是由函数和原型链机制模拟的。在我看来，原型链的核心只需要记住三点:

*   每个对象都有一个`__proto__`属性，指向它的原型对象。当调用实例的方法和属性时，如果在实例对象上找不到它，它将寻找原型对象。
*   构造函数的 prototype 属性也指向实例的 prototype 对象。
*   原型对象的构造函数属性指向构造函数。

# 1 新的模拟实现

首先，我们需要知道 new 的作用:

*   创建一个新对象并继承其构造函数的`prototype`。这一步是继承构造函数原型的属性和方法。
*   执行构造函数，方法中的`this`被指定为新的实例，这一步是执行构造函数中的赋值操作符。
*   返回一个新的实例(规范规定，如果构造函数返回一个对象，则返回该对象，否则返回第一步中创建的新对象)。

# ES5 是如何实现继承的

说到传承，最容易想到的就是 ES6 的`extends`。当然，如果只回答这个，就不合格了。我们需要从函数和原型链的角度实现继承。让我们一步一步地逐步实现一个合格的继承。

## 2.1 原型链继承

原型链继承的原理很简单。直接让子类的原型对象指向父类实例。当子类实例找不到相应的属性和方法时，它会寻找它的原型对象，即父类实例。实现父类的属性和方法的继承。

> 原型继承的缺点:

*   由于所有的`Child`实例原型指向同一个`Parent`实例，修改一个`Child`实例的父类引用类型变量将影响所有的`Child`实例。
*   在创建子类的实例时，不能向超类构造函数传递参数，也就是没有实现`super()`的功能。

## 2.2 构造函数继承

构造函数继承，即在子类的构造函数中执行父类的构造函数，并将子类的 this 与它绑定，这样父类的构造函数将成员属性和方法挂在子类的 this 上，这样不仅可以避免实例之间共享原型实例，还可以将参数传递给父类构造函数。

构造函数继承的缺点:不能继承父类原型上的属性和方法。

## 2.3 成分继承

既然原型链继承和构造函数继承有互补的优缺点，为什么不组合使用呢，于是就有了整合两者的组合继承。

组合继承的缺点:每次创建子类实例，都要执行两次构造函数(`Parent.call()`和`new Parent()`)。虽然这并不影响父类的继承，但是当子类创建一个实例时，原型中会有两个相同属性和方法的副本，这并不优雅

## 2.4 寄生成分遗传

为了解决构造函数执行两次的问题，我们将指向父类实例而不是指向父类原型，减去构造函数的一次执行

但是这种方法有一个问题。由于子类的原型和父类的原型指向同一个对象，所以我们对子类原型的操作会影响父类的原型。例如，向`Child.prototype`添加一个`getName()`方法将导致`Parent.prototype`也添加一个`getName()`方法或者被一个`getName()`方法覆盖。为了解决这个问题，我们对`Parent.prototype`做一个粗浅的复制。

至此，我们已经完成了 ES5 环境中继承的实现。这种继承方式被称为寄生组合继承，是目前最成熟的继承方式。巴别塔也用寄生组合继承对 ES6 继承进行了改造。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----913077e735bf--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----913077e735bf--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----913077e735bf--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----913077e735bf--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----913077e735bf--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----913077e735bf--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***