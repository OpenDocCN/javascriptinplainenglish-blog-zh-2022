# 作为一名 Web 开发人员需要掌握的 7 个功能概念

> 原文：<https://javascript.plainenglish.io/7-functional-concepts-to-master-as-web-developer-f51fdaf6e5c3?source=collection_archive---------2----------------------->

## 掌握这些关键概念，成为更好的 web 开发人员。

![](img/5a1a57e5ac733638cc9a3e79c7157c06.png)

Photo by [Sam Moqadam](https://unsplash.com/@sammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为 web 开发人员，我们乐于尝试各种不同的方法来构建 web 应用程序。使用函数是一件特别有趣的事情，但并不是每个人都充分利用各种函数概念来改进他们的代码，我将我在代码中经常使用的七个函数概念分离出来。

## 什么是功能概念？

功能概念是一组特定规则的一般概念，这些规则根据功能的行为或结构对不同类型的功能进行分类。利用这些概念将确保你写作

*   更容易维护和测试代码；
*   可重用代码；
*   功能更简单强大；
*   仅使用函数表示数据和操作；
*   等等；

函数式编程可能会变得超级复杂和紧张。取决于你想深入到什么程度，你会很快意识到仅仅用函数就可以做几乎所有的事情。有了如此惊人的能力，我发现自己一遍又一遍地使用这些概念来确保最佳代码。

## 纯函数

一个函数被认为是"*纯*"如果:

*   提供相同的输入，它复制相同的输出；
*   执行时无副作用；

更简单地说，如果我用两个数字调用一个函数，例如 3 和 8，并且这个函数每次都返回 11，而没有改变我的输入或环境中的任何东西(本地的或非本地的)，那么这个函数被认为是纯的。

**我们来看看几个不纯的函数:**

```
const x = 10;function **getTen**() {
   return x;
}
```

这个函数是不纯的，因为它直接访问一个作用域变量(不是赋予它的)，因此会产生不一致的结果。如果`x`改变，那么函数将改变它的返回。

```
function **getJrName**(personObj) {
  **personObj.name = `${personObj.name} Jr.`;** return personObj.name;
}
```

改变输入的函数不是纯函数。

```
function printSum(n1, n2) {
   **console.log(n1, n2);**
}
```

上述功能完全依赖于其环境。如果这个函数运行在`console.log`不存在或者行为不同的环境中，那么这个函数会产生不同的结果。

**那么如何保证自己有一个纯粹的函数呢？**

*   仅使用该功能提供的内容；
*   不要改变函数提供的任何东西；
*   不要直接访问环境、项目 API 或自定义实现；
*   对于相同的输入，总是产生相同的结果；

**为什么这对 web 开发人员如此重要？嗯，这些功能是如此可靠、安全、易于测试，它们将提高你所构建的一切的质量。此外，Javascript 可以在任何地方使用，在任何地方(服务器或客户端)使用相同功能的能力是一个值得利用的惊人特性。**

## 关闭

当你嵌套作用域时，你就创建了闭包，因为每个函数都有自己的作用域，嵌套函数将创建函数闭包，这些闭包是做各种事情的超级强大的函数。

以这个计数器为例:

```
const **createCounter** = (start = 0, inc = 1) => {
  let **count** = start;

  return () => {
    **count** += inc;

    return count;
  };
}
```

`createCounter`是一个函数，它接受两个参数，创建一个局部范围变量，并返回一个使用这些局部范围数据产生结果的新函数。

```
const **getNextCountUpByTwo** = **createCounter**(0, 2);**getNextCountUpByTwo**() // returns 2
**getNextCountUpByTwo**() // returns 4
**getNextCountUpByTwo**() // returns 6
**getNextCountUpByTwo**() // returns 8
```

闭包很棒，因为它允许您将数据与作用于该数据的函数相关联。它允许你在一定程度上模仿 OOP 类，因此闭包可以用在你需要对象的任何地方。

我一直使用闭包函数来模拟私有方法和属性，创建模块，并将数据和函数耦合在一起，就像你从上面的`counter`例子中看到的那样。

## 递归

我处理复杂的数据，如 [Three](https://medium.com/before-semicolon/introduction-to-the-tree-data-structure-16307e3f1967) 和 [Graph](https://medium.com/before-semicolon/graph-data-structure-implementation-in-javascript-668f291a8a16) 有时你无法完成——至少不容易——许多没有递归函数的读取和遍历。由于这个原因，递归成为我的代码中不可或缺的概念，以至于我经常发现自己在任何循环太复杂而难以理解的地方都能从中获得乐趣。

简单来说，递归就是如何在没有`while`和`for`循环的情况下循环。下面是一个使用递归的`forEach`函数的例子。

```
const **forEach** = (list, cb) => {
  if(list.length) {
    cb(list[0]);
    **forEach**(list.slice(1), cb)
  }
}**forEach**([2, 4, 6, 8], console.log) *// logs 2, 4, 6, 8*
```

递归函数是直接或间接调用自身的函数。它们不一定比普通的循环快，但是在复杂的循环中要容易得多。例如，看看用几行代码将 DOM 转换成 JSON three 是多么容易。

```
function **DOMtoJSON**(el) {
  return {
    nodeName: el.nodeName,
    type: el.nodeType,
    attributes: Array.from(
       el.attributes || [],
       (a) => ({name: a.name, value: a.value})),
    innerHTML: el.innerHTML,
    children: Array.from(el.childNodes, **DOMtoJSON**),
    textContent: el.textContent
  }
}const docBodyJSON = **DOMtoJSON(document.body)**
```

上面的递归将遍历整个文档体，一个元素一个元素地创建一个 JSON。用循环写同样的东西只是一段复杂得多的代码。

这就是递归的作用。当你完全理解并能在你的代码中自如地使用它们时，它们会带来巨大的不同。

## 绑定函数

在 web 开发中，绑定的概念被提到了很多，所以你必须至少理解它是关于什么的。

在函数式编程世界中，`bind`函数是一个将一段数据关联到一个创建新绑定函数的函数的函数。在 web 编程领域，我们经常听说将数据绑定到 DOM，这是将一段数据与一个特定的 DOM 元素相关联，这样当这段数据发生变化时，它就可以被更新。

这是一个可以利用的强大概念，因为它允许我们做超能力的事情，比如拥有读取调用功能，我们可以传递他们已经绑定的所有数据。

您可以像这样创建一个绑定函数:

```
function **bind**(fn, ...args) {
  return (...moreArgs) => fn(...args, ...moreArgs)
}
```

**注意**:绑定函数利用了将要创建的闭包概念

例如，如果我们有一个函数接受两个数字并返回它们的和，我们可以从它创建一个新的绑定函数，只接受第二个数字。

```
function **add**(a, b) {
  return a + b;
}const **addTwo** = **bind**(add, 2);**addTwo**(4); *// returns 6* **addTwo**(200); *// returns 202*
```

bind 函数是函数不可或缺的一部分，JavaScript 函数已经是现成的了。我们可以这样写上面的内容:

```
function add(a, b) {
  return a + b;
}const addTwo = **add.bind**(null, 2);**addTwo**(4); *// returns 6* **addTwo**(200); *// returns 202*
```

函数 [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) 方法将一个要用作`this`的对象作为第一个参数，并以逗号分隔的参数值列表。

Bind 肯定是需要习惯的东西，并尝试在代码中加入更多内容。我使用 bind 来传递绑定的函数，而不必指定调用它们的参数值。这允许我创建随时可用的回调函数，甚至是对我有利的劫持对象方法。

顺便说一下，这里有一个如何创建将数据绑定到元素并让您轻松更新数据的函数的示例。

```
function **bindElementData**(el, prop, value = '') {
  el[prop] = value;

  return (newValue) => {
    el[prop] = newValue;
  }
}const **btn** = document.querySelector('button#btn');
const **updateBtnText** = **bindElementData**(btn, 'textContent', 'my button');
const **updateBtnDisabled** = **bindElementData**(btn, 'disabled', false);**btn.onclick = () => {
  updateBtnText("btn clicked")
  updateBtnDisabled(true)
}**
```

## **咖喱功能**

当我向你介绍`bind`概念的时候，我已经向你展示了一个 curried 函数。Currying 一个函数是把它分解成更小的函数，每个函数接受一个参数。

例如，为了配合上面的`add`函数示例，它应该是这样的:

```
function add(a) {
  return (b) => {
    return a + b
  }
}
```

我们会这样称呼它:

```
*// all at once* **add**(4)(6); *// returns 10**// or by parts*const **addFourTo** = **add**(4);**addFourTo**(6) *// returns 10;*
```

那样做是不实际的，因为每次参数改变的时候，你都必须改变函数，这也不太好。为此，我们需要一个 currying 函数。一个为你服务的功能。

```
function **curry**(**func**) { **// 1**
  return function **curried**(...args) { 
    if (args.length >= **func.length**) { ***// 2***
      return **func**.**apply**(this, args); ***// 3***
    }

    ***// 4***
    return (...args2) => **curried**.**apply**(this, args.concat(args2))
  };
}
```

**注意**:curry 函数利用了**闭包**和**递归**等概念。

这里有很多东西需要解释，所以请允许我解释一下:

*   **1**:`curry`函数本身是一个纯粹的闭包函数，它将被 curried 的函数作为一个参数，并返回一个新的函数，该函数处理将参数应用于该函数。
*   **2** :在 JavaScript 中，一个函数有[的长度](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)，这里的长度是这个函数接受的参数的数量，不包括分布或者有默认值的参数——基本上是必需的参数。该语句检查是否提供了所有参数值。
*   **3** :应用函数的概念类似于绑定概念，不同之处在于它不是返回一个新的绑定函数，而是一次性绑定并调用函数。Apply 和 bind 一样，是内置在 Javascript 函数中的[。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
*   **4** :如果参数仍然与调用函数所需的参数数量不匹配，我们返回一个新函数，它收集其余的参数，当被调用时，它将新的和以前提供的参数应用于内部递归`curried`函数。

现在，如果我们的`add`函数接受更多的数字:

```
function **add**(a, b, c) {
  return a + b + c;
}
```

我们可以简单地保持它的原样，并用我们的`curry`函数创建一个新的咖喱版本:

```
const **curriedAdd** = curry(add);
```

我们可以这样称呼它:

```
*// all at once* **curriedAdd**(4)(6)(5); *// returns 15**// or by parts*const **addFourTo** = **curriedAdd**(4);
const **addTenTo** = **addFourTo**(6);**addTenTo**(5) *// returns 15;*
```

Currying 向您介绍了[懒惰评估](https://en.wikipedia.org/wiki/Lazy_evaluation#:~:text=In%20programming%20language%20theory%2C%20lazy,avoids%20repeated%20evaluations%20(sharing).)和[部分应用](https://en.wikipedia.org/wiki/Partial_application#:~:text=In%20computer%20science%2C%20partial%20application,producing%20a%20function%20of%20type%20.)的世界，这是需要学习的重要概念。它们允许您轻松地收集数据，并仅在需要时处理这些数据。

长表单处理就是一个很好的例子，在这种情况下，您懒洋洋地收集输入的信息，并验证它们，直到最后对信息采取行动。

当你不能一次得到所有的东西，或者只是简单地把事情分成小块，在中间做不同的动作，直到你准备好产生最终的结果时，奉承总是很棒的。

## 组合和管道函数

函数组合是将简单函数组合成更复杂函数的艺术。这意味着我们可以专注于把我们的功能分解得越小越好，然后像乐高积木一样把它们组合成我们想要的任何东西。这是一个非常有趣的概念。

在函数世界中，我们经常听说管道或组合函数是非常相似的概念。它们的工作方式相同，唯一的区别是它们执行所有功能的顺序和方向。Compose execute 从右边开始，pipe 从左边开始。两者都将使用前一个函数 return 来传递给下一个函数。

下面是如何使用 JavaScript 数组 [reduce 方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)创建这两者。

```
const **compose** = (...fns) => 
    x => fns.reduceRight((acc, fn) => fn(acc), x);const **pipe** = (...fns) => 
    x => fns.reduce((res, fn) => fn(res), x);
```

我更喜欢`pipe`这本书，因为它更容易阅读。如果你曾经和 RxJs 一起工作过，你就会知道管道的力量。我强烈建议进入那个世界。

使用`pipe`和`compose`函数向您介绍了一种编写函数的新方法。例如，这里有一个函数，给定一个数字列表，返回一个包含唯一偶数的列表。

```
const **getUniqueEvenNumbers** = **pipe**(
  list => new Set(list),
  Array.from,
  list => list.filter(n => n % 2 === 0)
);**getUniqueEvenNumbers(** [12, 54, 7, 33, 8, 90, 45, 22, 23, 8, 45, 54, 8, 12, 6]
);
*// returns [12,54,8,90,22,6]*
```

但是使用这种技术而不是强制性编码来创建函数的美妙之处在于，当您拥有一堆小函数时，您可以轻松地组合或通过管道连接在一起来创建整个应用程序。这需要对你如何编程做很多调整，所以我建议开始慢慢探索`pipe`和`compose`。

像 [Ramda](https://ramdajs.com/) 和 [RxJs](https://rxjs.dev/) 这样的库是很有意思的，尽管它们一开始可能感觉超级复杂。如果你更喜欢冒险，我建议你学习一点关于λ微积分的知识。你会惊奇地发现你可以单独用函数来表示程序中的一切。

## 结论

函数世界可能非常有趣，一开始可能会感觉有点复杂，但是作为任何开发人员，您都应该熟悉不同编程范例的基础知识，这样您就不会感到陌生。我使用一种混合风格，在这种风格中，我混合了许多函数式和面向对象的编程概念来尽可能多地构建东西。

理解并掌握这几个概念肯定会从总体上改变你的编程方式。它为我改变了。我更加小心翼翼，为了可重用性和测试的缘故，我发现自己尽可能地分解事物。总体而言，它无疑提高了代码质量。我试着在我的发现中寻找乐趣。

无论你的风格是什么，关键是享受并不断发现。

![](img/79122679204c8ac0aa65ca22857737ab.png)

**YouTube 频道** : [分号前](https://www.youtube.com/channel/UCrU33aw1k9BqTIq2yKXrmBw)
**网站**:[beforesemicolon.com](https://beforesemicolon.com/)