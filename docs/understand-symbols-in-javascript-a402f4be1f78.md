# 理解 JavaScript 中的符号

> 原文：<https://javascript.plainenglish.io/understand-symbols-in-javascript-a402f4be1f78?source=collection_archive---------13----------------------->

## 被低估的 JavaScript 特性。

![](img/25da1e536d6db22f1a9e4dbbcc797a52.png)

Photo by [Gabriel Heinzer](https://unsplash.com/es/@6heinz3r?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

让我们开始看看什么是符号:

*"一个* `*Symbol*` *是一个内置对象，它的构造函数返回一个* `*symbol*` [*原语*](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)*——也称为符号值或仅仅是一个符号——它保证是唯一的。"*——*MDN*

它们用于向对象添加唯一的属性键，而不会与其他代码添加的键冲突。

## **创建一个符号**

创建符号有三种主要方式:

1.  `**Symbol(string)**` 每次调用时，它都会返回一个新的**唯一的**符号。
    对调试有用的 ***描述*** 参数可以通过也可以不通过(打印带有`console.log()`的符号时显示)。
2.  `**Symbol.for(key)**`该操作在 ***符号注册表*** 中搜索具有给定关键字的现有符号，如果找到则返回，否则在*符号注册表*中创建一个具有给定关键字的新符号。与由`Symbol()`定义的符号不同，*符号注册表*中的符号是共享的，当你想在多个页面或模块间共享相同的*符号*时，这些符号非常有用。
3.  **使用标准库定义的符号:**有一些标准库定义的符号像`**Symbol.iterator**` **。**

## 比较符号

让我们看看当我们试图实例化两个符号并比较它们时会发生什么，每次你调用`Symbol('bar')`它都会创建一个新的符号，不管你是否传递了相同的描述，所以每次你比较两个实例时它们都会不同，相反，正如我们已经看到的，当你调用`Symbol.for('bar')`时，你在*符号注册表*中检索/创建符号，允许你通过键获得符号。

## 访问和迭代符号

当你遍历一个对象时，你会期望看到每个属性，但是由于符号键属性不像字符串键属性那样是可枚举的，所以你不会得到期望的属性，为了遍历符号，你需要像下面的例子中那样`Object.getOwnPropertySymbols`，它返回一个符号数组。

*我希望这是有帮助的，感谢阅读！*

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*