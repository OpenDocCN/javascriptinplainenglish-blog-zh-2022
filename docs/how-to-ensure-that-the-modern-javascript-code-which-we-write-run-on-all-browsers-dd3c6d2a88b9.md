# 如何确保我们的现代 JavaScript 代码能在所有浏览器上运行

> 原文：<https://javascript.plainenglish.io/how-to-ensure-that-the-modern-javascript-code-which-we-write-run-on-all-browsers-dd3c6d2a88b9?source=collection_archive---------2----------------------->

在我们讨论确切的解决方案之前，让我们先讨论一下如何得出解决方案。

所以问题是一些浏览器(准确地说是 JS 引擎)不能解析/理解我们写的代码。

好吧，那么如果我们把不可理解的代码转换成引擎可以理解/解析的代码呢？管用，对吧？

现在让我们看看如何做到这一点。

![](img/c94fec4759885128bd12b551abac9e4c.png)

Working on different browsers

进行这种转换有两种流行的方法。
1。Transpiler(针对基于语法的不规则性)
2。聚合填充(针对基于功能的不规则性)

酷，现在让我们逐一讨论

## 1.运输工具

这是一个将现代 JS 代码转换成 JS 语法的工具，也可以在过时的引擎上使用。请注意，这些软件通常可以接受各种语言的输入，例如，ReScript、TypeScript、CoffeScript 等，并发出 JavaScript。

例如:

ES6 中引入了类的使用

```
**class** Student {
    addStudent() {}   
    removeStudent() {}   
    **static** getOneStudent() {} 
}
```

然而，类只是 JS 中的语法糖，然而旧的浏览器会抛出不兼容错误，所以像 [*巴别塔*](https://babeljs.io/) 这样的编译器被用来将这种语法转换成原生 JS 代码(如下所示)，这些代码也可以被旧的浏览器/引擎解析。

```
**function** **Student**() {}  
Student.prototype.addStudent = **function** () {};  Student.prototype.removeStudent = **function** () {};  
Student.getOneStudent = **function** () {};
```

我们现在知道了语法转换在现代 JS 工具中是如何发生的，但是我们如何确保 ES 修订版中引入的内置函数也能在旧浏览器中很好地运行，并且即使这些浏览器还不支持它们也不会中断呢？

让我们来看看。:)

## 2.聚合填料

这是一段代码，它提供了我们作为开发人员期望浏览器本身提供的技术/功能。

注意，我们在这里关心的是新的函数/方法，我们不是在谈论语法变化，所以在这种情况下没有必要传输任何东西。我们只需要实现缺失的功能。

例如:

***Object.assign*** 是在 ES6 中引入的，所以我们应该编写它的 polyfill，以确保该功能在所有浏览器/引擎中无缝工作。

```
if (typeof Object.assign != 'function') {  
  Object.assign = function (target) {    
    'use strict';    
    if (target == null) {      
      throw new TypeError('Cannot convert undefined or null to object');    
    }         target = Object(target);    
    for (var index = 1; index < arguments.length; index++) {
      var source = arguments[index];
      if (source != null) {
        for (var key in source) {
          if (Object.prototype.hasOwnProperty.call(source, key)) {
            target[key] = source[key];
          }
        }
      }
    }
    return target;
  };
}
```

在这里看一下正在使用的主要聚合填充物[。](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills)

我希望我的解释能够帮助你理解这个概念。然而，我愿意接受各种反馈。你可以在 [LinkedIn](https://www.linkedin.com/in/jainlokesh318/) *上轻松联系到我。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*