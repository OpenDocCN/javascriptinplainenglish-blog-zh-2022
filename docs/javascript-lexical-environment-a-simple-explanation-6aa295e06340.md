# JavaScript 词汇环境:一个简单的解释

> 原文：<https://javascript.plainenglish.io/javascript-lexical-environment-a-simple-explanation-6aa295e06340?source=collection_archive---------12----------------------->

![](img/bb4ed5cec9771e5428b3063ddb1fe140.png)

Photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的词汇环境是一种包含标识符-变量映射的结构。换句话说，它是代码中声明的变量和常量的位置。

每个词法环境由一个环境记录和一个对外部词法环境的引用组成。标识符-变量映射存储在环境记录中，如果在当前词法环境中没有找到变量值，则使用对外部词法环境的引用来查找变量值。

当创建一个新的执行上下文时，就会创建一个词法环境。每当调用新的函数或代码块时，都会执行该过程。

例如，考虑以下代码:

```
function outer() {
  const x = 1;

  function inner() {
    const y = 2;
    console.log(x + y);
  }

  inner();
}

outer();
```

这段代码生成两个词法环境:一个用于`**outer**`函数，另一个用于`**inner**`函数。当您调用`**outer**`函数时，一个新的词法环境被创建，变量`**x**`被声明并用值`**1**`初始化。当调用`**inner**`函数时，一个新的词法环境被创建，变量`**y**`被声明并被设置为`**2**`。

因为变量`**x**`没有在`**inner**`函数中声明，JavaScript 在词法环境中搜索它。因为`**x**`是在词法环境之外声明的，所以它的值`**1**`在表达式`**x+y**` **中使用。**

为了提供 JavaScript 中词法环境如何工作的更具体的例子，让我们考虑下面的代码:

```
const x = 1;
let y = 2;

function outer() {
  const a = 3;
  let b = 4;

  function inner() {
    const c = 5;
    let d = 6;

    console.log(x + y + a + b + c + d);
  }

  inner();
}

outer();
```

这段代码有三个词法环境:全局环境、`**outer**`环境和`**inner**`环境。在脚本顶层声明的变量`**x**`和`**y**`存储在全局环境中。在`**outer**`函数中声明的变量`**a**`和`**b**`存储在`**outer**`环境中。最后，在`**inner**`函数中声明的变量`**c**`和`**d**`包含在`**inner**`环境中。

在这段代码中，标识符-变量映射的工作方式如下:

1.  当调用`**outer**`函数时，会为它创建一个新的词法环境。在这个环境中，标识符`**3**`被映射到变量`**a**`，标识符`**4**`被映射到变量`**b**`。
2.  当调用`**inner**`函数时，会为它创建一个新的词法环境。在这个环境中，标识符`**5**`被映射到变量`**c**`，标识符`**6**`被映射到变量`**d**`。
3.  表达式`**x + y + a + b + c + d**`在`**inner**`函数中计算。因为变量`**x**`和`**y**`没有在`**inner**`环境中声明，所以 JavaScript 在外部词法环境中搜索它们(`**outer**`函数)。表达式中使用了`**x**`和`**y**`，因为它们是在全局环境中声明的。因为变量`**a**`、`**b**`、`**c**`、`**d**`是在`**inner**`环境中声明的，直接使用它们的值。

为了更深入地解释词法环境及其工作原理，让我们考虑下面的代码:

```
const x = 1;
let y = 2;

function outer() {
  const a = 3;
  let b = 4;

  function inner() {
    const c = 5;
    let d = 6;

    function innermost() {
      const e = 7;
      let f = 8;

      console.log(x + y + a + b + c + d + e + f);
    }

    innermost();
  }

  inner();
}

outer();
```

这段代码有四个词法环境:全局环境、`**outer**`环境、`**inner**`环境和`**innermost**`环境。在脚本顶层声明的变量`**x**`和`**y**`存储在全局环境中。在`**outer**`函数中声明的变量`**a**`和`**b**`存储在`**outer**`环境中。在`**inner**`函数中声明的变量`**c**`和`**d**`存储在`**inner**`环境中。

最后，变量`**e**`和`**f**`在`**innermost**`函数中声明，并在`**innermost**`环境中找到。

在这段代码中，标识符-变量映射的工作方式如下:

1.  当调用`**outer**`函数时，会为它创建一个新的词法环境。在这个环境中，标识符`**3**`被映射到变量`**a**`，标识符`**4**`被映射到变量`**b**`。
2.  当调用`**inner**`函数时，会为它创建一个新的词法环境。在这个环境中，标识符`**5**`被映射到变量`**c**`，标识符`**6**`被映射到变量`**d**`。
3.  当调用`**innermost**`函数时，会为`**innermost**`函数创建一个新的词法环境。在这个环境中，标识符`**e**`被映射到变量`**7**`，标识符`**f**`被映射到变量`**8**`。
4.  表达式`**x + y + a + b + c + d + e + f**`在`**innermost**`函数中进行计算。因为变量`**x**`、`**y**`、`**a**`、`**b**`、`**c**`和`**d**`没有在`**innermost**`环境中声明，所以 JavaScript 在外部词法环境(`**inner**`函数)中搜索它们。表达式中使用了这些变量的值，因为它们是在`**inner**`环境中声明的。因为变量`**e**`和`**f**`是在`**innermost**`环境中声明的，所以直接使用它们的值。

这样，词法环境允许我们访问外部环境中声明的变量，并帮助确定 JavaScript 中变量的范围。理解词法环境可以帮助您编写更加高效、可维护和有效的 JavaScript 代码。

*我是一名 web 开发人员，* [*计算机智能研究员*](https://medium.com/@wiekiang) *带着探索科技与人文交汇点的热情。我有计算机科学的背景，对人工智能及其影响世界的潜力有浓厚的兴趣。*

无论我是在开发一个新的网络应用还是在人工智能领域进行研究，我总是在寻找方法来拓展可能性的边界，并对我周围的世界产生积极的影响。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

*****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。***