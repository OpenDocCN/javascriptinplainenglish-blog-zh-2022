# JavaScript 中的 Rest 参数语法和 Spread 运算符

> 原文：<https://javascript.plainenglish.io/rest-parameter-syntax-spread-operator-in-javascript-be8e83e9f02c?source=collection_archive---------2----------------------->

![](img/89ae1cd81280263f1088111835f2e810.png)

在本文中，我们将探索 JavaScript 提供的三点(`...`)语法。它的机制，以及为什么他们不是运营商。

本质上，三点语法用于两种机制:

*   接收数据的 Rest 语法。
*   为发送数据而扩展。

# 接收数据:rest 参数语法

rest 参数是一种特殊的参数，它通过数组接收函数调用的所有剩余参数:

```
function foo(first, ...rest) { 
  return { first, rest } 
}foo('a', 'b', 'c');// { first: 'a', rest: [ 'b', 'c' ] }
```

我们还可以在数组析构中使用 rest 语法:

```
const [head, ...tail] = ['a', 'b', 'c'];head
//'a'tail
// [ 'b', 'c' ]
```

我们可以用它来破坏对象:

```
const { first: f, ...rest} = {
  first: 'Petter', 
  last: 'Parker', 
  age: 19
};f
// 'Petter'rest
// { last: 'Parker', age: 19 }
```

# 发送数据:扩展运算符

在函数调用中使用 spread 运算符会将数组元素转换为函数调用参数。

```
function returnArgArray(...args) { 
  return args;
}returnArgArray(...['x', 'y', 'z']);
//[ 'x', 'y', 'z' ]
```

我们还可以将数组扩展成数组文字:

```
[...['a', 'b'], 'c']
// [ 'a', 'b', 'c' ]
```

我们可以将对象扩展成对象文字:

```
{...{ a:1, b:2 }, c:3}
// { a: 1, b: 2, c: 3 }
```

# Rest 和 spread 不是运算符

像`+`或`await`这样的运算符用于编写独立的表达式来计算值。我们可以在许多上下文中使用这些表达。

相比之下，休息和传播是它们周围环境的一部分。这就是为什么他们不应该被称为运营商:

*   Rest 语法:rest 参数(函数定义)，rest 元素(数组析构)，rest 属性(对象析构)
*   对于 spreading，我通常会说:“spreading into……”(函数调用、数组文字、对象文字)。

# 延伸阅读(用例等。)

Rest 语法:

*   [休息参数](https://exploringjs.com/impatient-js/ch_callables.html#rest-parameters)
*   [通过剩余元素进行解构](https://exploringjs.com/impatient-js/ch_destructuring.html#rest-elements)
*   [通过剩余属性进行析构](https://exploringjs.com/impatient-js/ch_destructuring.html#rest-properties)

传播:

*   [扩展成函数调用](https://exploringjs.com/impatient-js/ch_callables.html#spread-arguments)
*   [扩展成数组文字](https://exploringjs.com/impatient-js/ch_arrays.html#spreading-into-array-literals)
*   [扩展成对象文字](https://exploringjs.com/impatient-js/ch_objects.html#spreading-into-object-literals)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***