# 核心 JavaScript 预热

> 原文：<https://javascript.plainenglish.io/core-javascript-warm-up-part-1-ac34934589d4?source=collection_archive---------11----------------------->

## 第 1 部分:加强您对核心 JavaScript 概念的理解

![](img/d89b7a84dbd2ec818021631c21d95c2d.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将看到一些 JavaScript 问题，以预热和强化您的 JavaScript 核心概念。

我们把它作为一个系列来开始，在这里你会发现不同的问题列表及其解决方案。

让我们从一些令人惊讶的问题开始。

## 问题 1

以下代码的输出是什么？

```
**function** foo() { 
  let a = 1;
  return **function** () { 
    let b = 1; 
    console.log(++a, ++b); 
  }
} 
const bar = **foo();****bar();
bar();**
```

*提示:这是一个闭包函数*

**输出:**

```
2 2
3 2 
```

**bar()** 代表 foo 中定义的*闭包函数*。

"*闭包总是记得它的词法范围."*

' *a'* 的值始终由 bar()维护和引用；

而对于' *b'* ,它总是在函数调用时初始化，并保持不变。

所以每次函数被调用时，它都会初始化为 1。

## 问题 2

```
let obj = {  
  foo: "boo",
  a: **function** () {
    var b = this;
    console.log(this.foo);
    console.log(b.foo);
    (**function** () {
      console.log(this.foo);
      console.log(b.foo);
    })();
  }
} **obj.a();**
```

*提示:这是一个生命函数*

**输出:**

生命是一个独立的函数，对它来说“这”是一个全局变量。
所以输出是:

```
**boo
boo
undefined
boo**
```

**问题 3**

为下面给定的代码示例实现代码。

(使 calc 可以具有这些给定的函数，这些函数将返回 total 作为给定操作的值)

```
const result = calc.add(10).multiply(10).subtract(5).add(2);
console.log(result.total); // 97
```

*提示:你可以创建一个可重用的函数，而不需要函数之间的嵌套。*

**解决方案**

```
const calc = {  
  **total**: 0,
  **add**: **function** (a) {
    this.total += a;
    return this;  
  },
  **multiply**: **function** (a) {
    this.total *= a;
    return this;  
  },
  **subtract**: **function** (a) {
    this.total -= a;
    return this;
  }
}
```

**问题 4**

以下代码的输出是什么？

```
let x = true;
let count = 0;setTimeout(() => {
  x = false;
}, 2000);setInterval(() => {
  if (x) {
    console.log(count++)
  }
}, 200);
```

提示:“x”将在 2 秒后为假，直到 setInterval 可以执行。

**输出:**

```
0
1
2
3
4
5
6
7
8
```

因为计数器将增加 200 毫秒。因此，直到条件变为 ***假*** *，*需要 2000 毫秒。因此，它将总共打印 9 次= 1800 毫秒(每次 200 毫秒)，最后一次，在 2000 毫秒时，条件将为假。

**问题 5**

以下代码的输出是什么？

```
var x = 21;
var fun1 = function () {
  console.log(x);
  var x = 20;
}fun1();
```

*提示:在 JavaScript 中叫做提升*

**注意:**对于那些不熟悉 JavaScript 中的提升的人来说，根据 [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) ，提升“是指解释器在执行代码之前，将函数、变量或类的*声明*移动到其作用域顶部的过程。”

**吊装示例**

```
console.log(x); // x is undefined because it is declared as 'var'
var x = 10;console.log(y);
let y = 10; // y will throw reference error because it is declared as 'let' and 'let' is hoisted in temporal deadzoneconsole.log(z);
const z = 10; // z also will throw reference error because it is declared as 'const' and 'const' is hoisted in the temporal deadzone
```

**输出:**

既不是 20 也不是 21 而是**未定义**。

这里，我们想将 x 的值赋为 20，但在赋值之前，**它将被提升，var 的默认值未定义**。

你们中的许多人可能会问它是 var，既然它有全局访问权，x 在全局上是 21，那么为什么它没有被记录为 21 呢？

这背后的原因是如果去掉 x = 20 从 **fun1()** ，开始就不再被吊起。因此，它将记录为 21。

然而，我们在全局范围内将它声明为 21，但我们仍然将它放在 fun1()中。这就是为什么它被默认为未定义。

# 结论

我希望你喜欢阅读和学习新的东西。我们已经开始了这个系列，将会涵盖更多的例子/问题，帮助 JavaScript 开发人员更深入地了解核心概念，并帮助复习高级概念。

我写过一些常见的 JavaScript 错误和最佳实践[第一部分](https://hardik-thakar.medium.com/basic-javascript-mistakes-and-best-practices-aa97ffc0e553)和[第二部分](https://hardik-thakar.medium.com/part-2-common-javascript-mistakes-and-best-practices-8d60b210617e)，涵盖了更多的概念。

如果有任何建议、意见或疑问，请随时联系我，发表评论。谢谢你。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***