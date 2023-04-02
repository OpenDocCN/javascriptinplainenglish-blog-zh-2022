# 大多数开发人员不知道的 6 个很酷的现代 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/6-cool-modern-javascript-features-most-developers-dont-know-about-7b1dbf43d7e0?source=collection_archive---------0----------------------->

## 编写简明 JavaScript 代码的技巧

![](img/6f7f9959b65f75351a04409baf535b29.png)

# 前言

JavaScript 在不断进化升级，越来越多的新特性让我们的代码变得简洁。本文将介绍六个新的 JavaScript 特性。让我们一起来研究它们。

# 1.使用“Object.hasOwn”而不是“in”运算符

有时，我们想知道一个属性是否存在于一个对象上，并使用“in”操作符或“obj.hasOwnProperty”来这样做。但两者都有一些瑕疵，我们来看看。

**“in”运算符**

如果指定的属性在`specified object` 或其`prototype chain`中，则“in”运算符返回`true`。

**obj.hasOwnProperty**

`hasOwnProperty`方法返回一个布尔值，表明对象是否有指定的属性作为它的`own property`(与继承它相反)。

**使用上面相同的例子:**

也许`"obj.hasOwnProperty"`已经可以过滤掉原型链上的属性了，但是在某些情况下并不安全，会导致程序失败。

**Object.hasOwn**

不用担心，我们可以用“Object.hasOwn”来避免这两个问题，比“obj.hasOwnProperty”方法更方便，也更安全。

# 2.使用“#”声明私有属性

过去，我们使用`"_"`来表示私有属性，但是它并不安全，仍然可能被外部修改。

**我们可以使用“#”来实现真正安全的私有属性:**

# 3.有用的数字分隔符

我们可以用“_”让数字更易读。很酷。

当然，我们可以使用“_”进行实际计算。

# 4.用“？."简化“&&”和三元运算符

下面的例子你一定很熟悉，我们可以简化一下吗？

用“？."简化您的代码。

**提示**

“的常见拼法？."

1.  `obj?.prop`对象属性
2.  `obj?.[expr]`对象属性
3.  `func?.(...args)`函数或对象方法的调用

# 5.用“？?"而不是“||”

用“？?"代替“||”，用来判断运算符左边的值是`null`还是`undefined`，然后返回右边的值。

# 6.使用“BigInt”支持大整数计算问题

JS 中超过`"Number.MAX_SAFE_INTEGER"`的数字计算不保证正确。

**例如:**

对于大数的计算，可以使用“BigInt”来避免计算错误。

# 最后

**感谢阅读。**我期待期待您的关注和阅读更多高质量的文章。

[](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/my-boss-you-dont-know-react-at-all-f493970f1807) [## 我老板:你根本不知道反应！😠

### 你必须知道的 React 的 3 种错误用法。

javascript.plainenglish.io](/my-boss-you-dont-know-react-at-all-f493970f1807) [](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [## 让你看起来像高级开发人员的 8 个很酷的 GitHub 技巧

### 使用 GitHub 可以做的 8 件很酷的事情

javascript.plainenglish.io](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/what-does-123-tostring-length-123-print-out-in-javascript-2c804a414325) [## 123['toString']。length + 123)用 JavaScript 打印出来？

### 95%的前端开发者回答错误的问题。

javascript.plainenglish.io](/what-does-123-tostring-length-123-print-out-in-javascript-2c804a414325) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*