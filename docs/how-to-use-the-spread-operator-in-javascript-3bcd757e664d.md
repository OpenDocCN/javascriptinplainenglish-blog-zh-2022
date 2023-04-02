# 如何在 JavaScript 中使用 Spread 运算符

> 原文：<https://javascript.plainenglish.io/how-to-use-the-spread-operator-in-javascript-3bcd757e664d?source=collection_archive---------4----------------------->

![](img/f79f551412ea90ab8f158b8f28b81c02.png)

Photo by [insung yoon](https://unsplash.com/@insungyoon?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) / [Unsplash](https://unsplash.com/?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit)

JavaScript 语言中最有用的操作符之一也是最难理解的。JavaScript 中的 spread 操作符表示为`...`，它允许您*就地扩展*数组或可迭代对象的元素，并可以帮助您以几种不同的方式编写更干净、更简洁的代码。

尽管从概念上讲，spread 运算符总是用于“扩展”数组或可迭代对象，但实际用法和行为会因上下文而有所不同。在这篇文章中，我们将看看 JavaScript 的 spread 操作符，以及它的许多不同用法。

# JavaScript 中的 Spread 运算符是什么？

简单地说，JavaScript 中的 spread 操作符扩展了数组或可迭代对象的元素。它可以用来解决几个不同的问题:

*   从数组和对象中提取值
*   复制数组和对象
*   添加或删除元素
*   用数组中的参数调用函数
*   用可变参数定义函数。

虽然这些用例在概念上都是相似的，但是如何应用 spread 操作符的具体细节在不同的用例之间有所不同。

注意，spread 操作符处理数组和*可迭代*对象。虽然 JavaScript 中可能遇到的大多数对象都是可迭代的(包括像`value = {a: 1, b: 2, c: 3}`这样的对象文字)，但是一些 API 可能会返回不可迭代的对象。在本文的其余部分，当我们提到*对象*并使用 spread 操作符时，我们特指*可迭代*对象。

也就是说，让我们深入研究使用 spread 操作符的各种方法！

## 从对象或数组中提取值

spread 运算符通常与对象或数组*析构一起使用。*析构是指我们使用特殊的赋值语法来解包对象或数组的元素。

在这个简单的例子中，我们*将*一个 5 元素数组析构为 3 个变量:第一个值赋给`a`，第二个值赋给`b`，列表的其余部分赋给`rest`:

```
> array = [10, 20, 30, 40, 50] 
> let [a, b, ...rest] = array 
> a 
10 
> b 
20 
> rest 
[ 30, 40, 50 ]
```

我们可以对对象做一些非常类似的事情:我们可以通过键提取特定的值，并将对象的剩余部分提取到不同的变量中:

```
> values = {x: 10, y: 20, z: 30} 
> let { x: xValue, ...rest } = values 
> xValue 
10 
> rest 
{ y: 20, z: 30 }
```

注意扩展操作符和“剩余”参数实际上并不是析构所需要的 T21——但是它们很常见。如果您实际上不关心对象或数组的其余部分，您可以在没有 spread 运算符的情况下进行析构:

```
> array = [10, 20, 30] 
> [a] = array 
> a 
1 

> values = {x: 10, y: 20, z: 30} 
> let { x: xValue } = values 
> xValue 
10
```

如果您使用 React，您可能会看到这种模式被用来从`props`对象中提取某些*属性*，并传递其余的属性。考虑一个简单的`WrappedImage`组件，它只是在`img`标签周围应用了一个`Wrapper`:

```
const WrappedImage = ({ backgroundColor, ...rest }) => { 
  return ( 
    <Wrapper color={backgroundColor}>
      <img {...rest} /> 
    </Wrapper> 
  ) 
}
```

在这种情况下，我们提取`Wrapper`的`backgroundColor`道具，并将所有剩余的属性传递给`img`。我们不关心解开一个`img`标签可以接受的所有属性——除了`backgroundColor`之外，任何传入我们组件的内容都将原封不动地通过。

# 从数组或对象中移除值

细心的读者会注意到，上面的代码通过用 spread 操作符提取“rest”值，也具有生成移除了元素的数组和对象的效果:

```
> let array = [1, 2, 3] 
> let [ _value, ...rest ] = array 
> rest
[2, 3]
```

在上面的例子中，我们将第一个参数提取到一个名为`_value`的变量中。下划线是约定俗成的用法，表示我们并不真正关心一个值——它只是一个占位符。

# 向数组或对象添加值

使用 spread 操作符的另一种方法是将*元素添加到一个对象或数组中。*

首先，让我们在数组末尾添加一个值:

```
> let numbers = [1, 2, 3] 
> newNumbers = [...numbers, 4] 
[ 1, 2, 3, 4 ]
```

我们可以在数组的开头或结尾都进行扩展——甚至可以同时在两个地方进行扩展！

```
> let numbers = [1, 2, 3] [ 1, 2, 3 ] 
> newNumbers = [0, ...numbers, 4] 
[ 0, 1, 2, 3, 4 ]
```

甚至可以使用多个扩展运算符来组合数组:

```
> let n1 = [ 1, 2, 3 ] 
> let n2 = [ 4, 5, 6 ] 
> [ ...n1, ...n2 ] 
[ 1, 2, 3, 4, 5, 6 ]
```

同样的技术也适用于对象。我们可以通过应用 spread 操作符来扩展对象，然后提供附加的键和值:

```
> values = {x: 10, y: 20, z: 30} 
> newValues = {...values, a: 10} 
{ x: 10, y: 20, z: 30, a: 10 }
```

然而，对于对象，有一点需要注意，那就是重复键的顺序很重要。当密钥重复时，右边的优先:

```
> values = {x: 10, y: 20, z: 30} 

> // The new value for x takes precedence: 
> newValues = { ...values, x: 50} 
{ x: 50, y: 20, z: 30 } 

> // The old value for x takes precedence: 
> newValues = { x: 50, ...values } 
{ x: 10, y: 20, z: 30 }
```

就像数组一样，我们可以使用 spread 操作符的多个实例来组合对象。如上所述，在出现重复键的情况下，键的最右边的值优先:

```
> v1 = {x: 10, y: 20, z: 30} 
> v2 = {w: 40, y: 50} 
> { ...v1, ...v2 } 
{ x: 10, y: 50, z: 30, w: 40 }
```

# 复制数组或对象

以同样的方式，使用扩展操作符提取值的*可以有效地用于从数组或对象中移除元素，扩展操作符也可以用于*复制*数组或对象。这在你处理不应该被修改的不可变的 T21 数据时特别有用。*

例如，状态管理库 Redux 指定:

> *【减速器】不允许修改已有的* `*state*` *。相反，他们必须通过复制现有的* `*state*` *并对复制的值“*”进行更改，来进行不可变更新

*考虑一个函数，它被设计成以不可变的方式增加对象中的值。spread 运算符可用于轻松复制和更新值，而不是修改它:*

```
*// 🚫 Don't modify the existing state 
const incrementValue = (state) => { state[value] += 1 return state } 

// ✅ Use the spread operator to copy the state 
const incrementValue = (state) => { return {...state, state.value + 1} }*
```

# *使用数组中的参数调用函数*

*spread 运算符也可用于将参数从数组传递给函数。考虑这样一个场景，我们将想要传递给函数的参数存储在一个数组中:*

```
*> function add(x, y, z) { return x + y + z } 
> numbers = [1, 2, 3] 
> add(...numbers) 
6*
```

*像 spread 操作符的一些其他用法一样，这不是从数组中传递参数函数的唯一方法。我们可以手动解包这些值，或者我们可以在一个函数上使用 *apply* 方法来完成同样的事情:*

```
*> // manually unpack the values from an array 
> add(numbers[0], numbers[1], numbers[2]) 

> // use apply() to pass in arguments from an Array 
> add.apply(null, numbers)*
```

# *定义具有可变参数的函数*

*最后，spread 运算符可用于定义一个函数，该函数采用可变数量的参数。假设我们想要定义一个函数，它可以被称为`f(1)`、`f(1,2)`、`f(1,2,3)`，等等。在函数定义中使用 spread 运算符，将所有参数打包到一个数组中:*

```
*> function f(...args) { console.log(args) } 
> f(1, 2, 3) 
[ 1, 2, 3 ]*
```

*与 spread 运算符的其他用法类似，它可以出现在其他参数列表的末尾:*

```
*> function f(x, ...args) { console.log(args) } 
> f(1, 2, 3) 
[ 2, 3 ]*
```

*spread 运算符的这种用法不太常见，但是对于某些 API 非常有用。例如，JavaScript 的`console.log()`函数接受可变数量的参数，让我们在一次调用中记录多个值。*

*值得注意的是，变量参数也可以使用函数内部可用的特殊的`arguments`对象来实现，所以并不是每个接受变量参数的函数都使用 spread 运算符。*

# *想了解更多？*

*如果您想快速参考 JavaScript 中的 spread 操作符，请务必查看我们的 [JavaScript 视频备忘单](https://www.youtube.com/channel/UCOw1-AGy_tHnbjiwC4EdFVw)主题:*

*   *查看我们关于 JavaScript 数组的 `[map()](https://blixtdev.com/javascript-video-cheatsheets-map-and-reduce-with-arrays/)` [和](https://blixtdev.com/javascript-video-cheatsheets-map-and-reduce-with-arrays/) `[reduce()](https://blixtdev.com/javascript-video-cheatsheets-map-and-reduce-with-arrays/)` [的](https://blixtdev.com/javascript-video-cheatsheets-map-and-reduce-with-arrays/)[视频备忘单](https://blixtdev.com/javascript-video-cheatsheets-map-and-reduce-with-arrays/)*
*   *看看[我们最喜欢的 JavaScript 书籍之一](https://amzn.to/3jgxPiD)*
*   *查看我们的一些[其他 JavaScript 文章](https://blixtdev.com/tag/javascript/)*

**原载于 2022 年 12 月 20 日*[](https://blixtdev.com/how-to-use-the-spread-operator-in-javascript/)**。这篇文章可能包含附属链接。***

***更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*******

*****有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***