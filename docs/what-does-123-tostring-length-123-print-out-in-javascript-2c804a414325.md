# 123['toString']。length + 123)用 JavaScript 打印出来？

> 原文：<https://javascript.plainenglish.io/what-does-123-tostring-length-123-print-out-in-javascript-2c804a414325?source=collection_archive---------0----------------------->

## 95%的前端开发者回答错误的问题。

![](img/7a0492a70c6c504ef83b943ff7a49a27.png)

# 前言

前一段时间，我被问到一个简单的面试问题，但我没有给出正确的答案，在开始，甚至 95%的前端开发人员都无法准确回答。面试问题是什么？让我们看一看…

一开始我以为答案是`126(3 + 123)`，但是我错了。真正的答案是什么？让我们一步步揭开谜底。

# 函数的形参数量

这很容易。所有前端开发者都知道答案。

`function`的参数与其长度一样多。但事实真的是这样吗？跟着我，继续往下看...

# 默认参数

这让我很震惊，甚至看起来和上面的答案有些不同。是的，我们可以从这里得出一个结论:

`*function.length*` *是第一个带默认值的参数前的个数。*

# 该函数的其余参数

如果一个函数有剩余的参数，如何计算“function.length”？

是的，我肯定你是对的。答案是`1`。所以我们可以得出另一个结论:

*其余参数不包括在“function.length”的计算中。*

# 摘要

最后，你知道这个问题的答案吗？

看一下 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length) 上的摘要

*长度是函数对象的一个属性，表示函数需要多少个自变量，即形参的数量。*

*该数字不包括其余参数，仅包括第一个参数之前的参数，并具有默认值。*

*相反，* `*arguments.length*` *是函数的局部变量，提供实际传递给函数的参数个数。*

# 最后

**感谢阅读。**期待期待您的关注和阅读更多高质量的文章。

[](/6-cool-modern-javascript-features-most-developers-dont-know-about-432f7652dd4c) [## 大多数开发人员不知道的 6 个很酷的现代 JavaScript 特性

### 编写简明 JavaScript 代码的技巧

javascript.plainenglish.io](/6-cool-modern-javascript-features-most-developers-dont-know-about-432f7652dd4c) [](/9-ways-to-make-a-1-a-2-a-3-true-in-javascript-c2e1903b24b) [## 在 JavaScript 中实现(a==1 && a==2 && a==3) === true 的 9 种方法

### 是的，这可能是真的，而且有 9 种方式——太神奇了！

javascript.plainenglish.io](/9-ways-to-make-a-1-a-2-a-3-true-in-javascript-c2e1903b24b) [](/interviewer-you-have-been-working-for-3-years-and-you-cant-answer-this-algorithm-question-5f79cba18e06) [## 面试官:你工作 3 年了，这种算法题你都不会答？

### 一个女生的面试经历

javascript.plainenglish.io](/interviewer-you-have-been-working-for-3-years-and-you-cant-answer-this-algorithm-question-5f79cba18e06) [](/8-javascript-tricks-to-make-you-a-better-programmer-948b5a3c35b4) [## 让你成为更好的程序员的 8 个 JavaScript 技巧

### 使用这些代码提示，让您的 JavaScript 更具可读性和可扩展性。

javascript.plainenglish.io](/8-javascript-tricks-to-make-you-a-better-programmer-948b5a3c35b4) [](/my-boss-you-know-es6-but-why-dont-you-use-it-5e0316f14c67) [## 我老板:你知道 ES6，为什么不用？😠

### 老板的 10 条抱怨让我受益匪浅。

javascript.plainenglish.io](/my-boss-you-know-es6-but-why-dont-you-use-it-5e0316f14c67) [](/15-killer-websites-for-web-developers-35a4c007942a) [## 面向网络开发人员的 15 个黑仔网站

### 99.9%的开发者都不知道。

javascript.plainenglish.io](/15-killer-websites-for-web-developers-35a4c007942a) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*