# 6 个意想不到的 JavaScript 问题

> 原文：<https://javascript.plainenglish.io/6-unexpected-javascript-problems-50d7dc6493e7?source=collection_archive---------12----------------------->

## 关于前端你应该知道的 6 个问题。

![](img/47c5e3861cf68ce670962c91f8f06001.png)

Photo by [Sergey Pesterev](https://unsplash.com/@sickle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为前端开发工程师，JavaScript 是我们主要的开发语言。它有相对简单的语法和完善的生态系统，在社区中越来越有影响力。在使用的过程中，我们经常会遇到各种奇怪的问题，这些问题经常让我们困惑。所以我列出了 6 个常见而有趣的问题。

## 1.奇怪的尝试…捕捉行为

问题:下面的代码执行时会返回什么，2 还是 3？

答案是 3。这是为什么呢？这是因为在 try…catch…finally 语句中，无论是否引发异常，finally 子句都会执行。此外，如果引发异常，即使没有处理异常的 catch 子句，finally 子句中的语句也会执行。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) [## try…catch — JavaScript | MDN

### try…catch 语句由 try 块和/或 catch 块、finally 块组成。中的代码…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) 

## 2.[]和 null 都是对象

下面 3 行代码的结果是什么？

返回的结果是这样的。

typeof 运算符返回一个字符串，并且必须符合表 37: typeof 运算符返回值。它为空、普通对象、标准特定对象和不实现[[Call]]的非标准特定对象返回字符串“object”。

但是，您可以使用 toString 方法来检查对象的类型。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) [## 类型 of — JavaScript | MDN

### typeof 非常有用，但它并不像所要求的那样通用。例如，typeof []，是' object '，以及…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) 

## 3.arrow 函数返回 undefined

为什么函数 f2 执行后返回 undefined？

我们的第一印象应该是返回{}，但是它返回 undefined，本质上是因为 arrow 函数返回{}是 arrow 函数语法的一部分，{}不返回，所以默认返回 undefined。我们可以写一个测试用例来看看。

所以上面的 f2 函数返回 undefined，尽管如果需要，只需将返回值括在括号中，就可以返回一个{}对象。

```
let f2 = () => ({});
f2(); *// -> {}*
```

## 4.我们也可以使用反引号来执行函数吗？

除了下面的方法，还有其他方法调用函数吗？

当然，我们可以使用“反报价”调用。

这看起来很神奇，但它实际上使用了一个模板字符串。这是模板字符串的高级形式，带有标签的模板字符串。在上面的示例代码中，f 函数是模板文字标签。标签可用于解析函数模板字符串。tag 函数的第一个参数包含一个字符串值数组。其余参数与表达式相关。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) [## 模板文字(模板字符串)— JavaScript | MDN

### 在普通模板文本中，允许使用以下转义序列:以\u 开头的 Unicode 转义，例如…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) 

## 5.JavaScript 里有标签？

下面这种写法会不会有问题？

答案是否定的，它会返回 Hello 字符串。这是因为 foo 被识别为标签然后执行，后面跟着 console . log(“Hello”)然后 break foo 中断执行。我们经常使用带标签的语句和 break/continue 语句来结束或继续循环。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) [## 标签— JavaScript | MDN

### 您可以使用标签来标识循环，然后使用 break 或 continue 语句来指示程序是否…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) 

## 6.{}{}未定义

我们可以在控制台中测试以下代码。像这样的结构将返回最后定义的对象的值。

解析到{}时，返回 undefined，解析到{foo: 'bar'}{}时，表达式{foo: 'bar'}返回' bar '。

这里的{}有两个意思:表示“对象”或者表示“代码块”。

例如()=> {}中的{}表示“代码块”。所以我们要加上括号:()=> ({})才能让它正确返回一个对象。

所以，如果我们现在使用{foo: 'bar'}作为一个“块”，我们可以在终端中写这个。

啊哈，结果一样！所以{foo: 'bar'}{}中的括号表示“代码块”。

***欢迎关注我上***[***Twitter***](https://twitter.com/yanghui0324)*[***LinkedIn***](https://www.linkedin.com/in/hui-yang-075076245/)***，以及***[***GitHub******！***](https://github.com/guchen-yh)*

*写作一直是我的激情所在，它给了我帮助和激励他人的快乐。如果您有任何问题，请随时联系我们！*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。****