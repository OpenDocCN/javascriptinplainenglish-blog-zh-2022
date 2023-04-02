# 神秘的 JavaScript 问答&采访中经常被问到的问题

> 原文：<https://javascript.plainenglish.io/can-you-solve-these-javascript-mysteries-b439db2dd0df?source=collection_archive---------4----------------------->

## 这些 JavaScript 的神秘问题有时会在面试中被问到。在这里找到答案。

![](img/2acda9f7a54c6fcac5f7a1a4643d49e3.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这些 JavaScript 的神秘问题有时会在面试中被问到。你知道答案吗？

# 知道为什么 Math.max()在不传递参数的情况下返回-Infinity 吗？

Math.max()是一个 JavaScript 实用函数，它从参数中返回最大的数字。

```
Math.max(1, 2, 3); // => 3Math.max(1); // => 1Math.max(); // => -Infinity
```

在理解这个秘密之前，知道如何对数组使用这个函数是至关重要的。我们需要使用 spread 操作符来使用数组。

```
const numbers1 = [1, 2, 3];Math.max(…numbers1); // => 3
```

上面代码中的 Math.max(…numbers1)使用了 spread 运算符。该表达式返回 numbers1 数组的最大数量:3。

要对两个数组使用 Math.max，只需用 spread 操作符传递两个数组:Math.max(…arr1，…arr2)。

现在，真正的乐趣开始了。尝试使用 spread 运算符将空数组传递给 Math.max。

```
const numbers1 = [];Math.max(…numbers1); // => -Infinity
```

当不带任何参数调用时，Math.max()返回-Infinity 以处理需要多个最大值运算的情况(max of max of max of max…)。用扩展运算符传递空数组与不带参数调用相同。

类似地，当没有传递参数时，Math.min()将返回无穷大。

# 你知道 parseInt(0.0000005)为什么返回 5 而不是 0 吗？

parseInt(strNumber)总是将第一个参数转换为字符串(如果它不是字符串)，然后将该数字字符串解析为整数值，并使用浮点值(如 0.5、0.05 等)调用 parseInt，返回 0。让我们来解开这个谜。

首先，将给定的值转换成字符串。所以当字符串转换时会是:String(0.0000005)；// => '5e-7 '。

parseInt('5e-7 ')的输出将=> 5。

类似地，parseInt(5e-7)的输出也将=> 5。

所以当你调用 parseInt(0.0000005)时，你调用的是 parseInt(5e-7)。

# 你知道 JavaScript 里什么是密集数组和稀疏数组吗？

```
const names = [‘Batman’, ‘Joker’, ‘Bane’];
```

在上面的代码中，names 数组是密集的。密集数组在每个索引处包含项目，从 0 开始直到 names . length-1。

```
const names = [‘Batman’, , ‘Bane’];
```

在上面的例子中，names 数组创建了一个稀疏数组。这是因为它在索引 1 处有一个洞。如果您在 names[1]处访问的值，它的计算结果为 undefined。

现在你知道了。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***