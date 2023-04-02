# JavaScript 的 parseInt(0.0000005)为什么打印“5”？

> 原文：<https://javascript.plainenglish.io/why-does-javascripts-parseint-0-0000005-print-5-63c684e186af?source=collection_archive---------2----------------------->

## JavaScript 中 parseInt(0.0000005)为什么打印 5？一个很神奇的问题！

![](img/04ea54b52638cb5476f1ae4736f040e9.png)

# 前言

最近我在开发一个项目的时候遇到了一个奇怪的问题，`parseInt (0.0000005) === 5`😱。正常情况下，输出 0 是正确的，但为什么是 5 呢？让我们一起来探讨这个问题。

# 1.什么时候使用 parseInt？

首先，你一般什么时候用`parseInt`？大多数时候，我们用它来解析一个**字符串**并返回它的**整数部分**。带着这个问题，我们来看看 parseInt 方法。

# 2.关于 parseInt 的一些事情

根据 MDN [文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)，*“parse int(string，radix)函数解析一个字符串参数并返回一个指定基数(数学数系中的基数)的整数。”*

**语法**

```
parseInt(string)
parseInt(string, radix)
```

**示例**

```
parseInt('0.5') // 0
parseInt('0.5') // 0
parseInt('0.05') // 0
parseInt('0.005') // 0
parseInt('0.0005') // 0
parseInt('0.00005') // 0
parseInt('0.000005') // 0
parseInt('015') // 15
parseInt('015', 8) // 13
parseInt('15px', 10) // 15
```

# 3.parseInt 如何转换数字？

当 parseInt 的第一个参数是一个数字时，如何解析？

`parseInt(0.0000005) === 5`的真相也在这里...

# 3.1.第一步？将数字转换为字符串。

让我们使用字符串函数检查基于字符串的值，看看每个值的输出是什么:

```
String(0.5);      // => '0.5'
String(0.05);     // => '0.05'
String(0.005);    // => '0.005'
String(0.0005);   // => '0.0005' 
String(0.00005);  // => '0.00005'
String(0.000005); // => '0.000005'
String(0.0000005); // => '5e-7' pay attention here
```

# 3.2.第二步，做舍入运算。

正如用户 [SeyyedKhandon](https://stackoverflow.com/users/12666332/seyyedkhandon) 在他的堆栈溢出[回答](https://stackoverflow.com/questions/69613606/why-does-javascripts-parseint0-0000005-print-5)中解释的:

“当我们使用`parseInt(0.0000005)`时，它等于`parseInt('5e-7')`，根据定义:

> parseInt 可能只将字符串的前导部分解释为整数值；它忽略任何不能被解释为整数符号的一部分的代码单元，并且没有给出任何这样的代码单元被忽略的指示。

```
parseInt(0.0000005)
```

```
parseInt('5e-7') // 5
```

**最后，答案将只返回 5，因为它是在非字符 e 之前唯一的数字字符，所以它的其余部分 e-7 将被丢弃。”**

# 4.如何安全获取浮点数的整数部分？

建议使用以下 Math.floor()函数:

```
Math.floor(0.5);      // => 0
Math.floor(0.05);     // => 0
Math.floor(0.005);    // => 0
Math.floor(0.0005);   // => 0
Math.floor(0.00005);  // => 0
Math.floor(0.000005); // => 0
Math.floor(0.0000005); // => 0
```

# 5.类比学习

现在，你能解释为什么`parseInt(99999999999999999999999999)`等于 1 吗？

# 最后

感谢阅读。我期待着您的关注和阅读更多高质量的文章。

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

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****