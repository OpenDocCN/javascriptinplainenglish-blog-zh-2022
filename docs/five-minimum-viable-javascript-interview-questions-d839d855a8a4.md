# 五个最低可行的 Javascript 面试问题

> 原文：<https://javascript.plainenglish.io/five-minimum-viable-javascript-interview-questions-d839d855a8a4?source=collection_archive---------9----------------------->

## 面试官:问他们你的面试是不是快没时间了。签证人:如果你的准备时间快用完了，就练习一下。

*这是我的* [*五个最起码可行的面试问题系列*](https://medium.com/50ld/five-minimum-viable-interview-questions-series-e8531b5f7db2) *的一部分，在这里我研究并整理了每个面试题目的五个基本面试问题。所有这些问题都旨在评估工作中需要的实际技能*

如今，公司招聘全栈职位是很常见的。一个全栈开发人员通常会同时从事前端和后端开发。同样的期望也适用于面试。

因此，要想获得一个全栈职位，面试或被面试都很难。会有太多的问题要问或准备。但是如果你快没时间了，这里有五个问题我觉得你应该知道。

![](img/30a99320cce8c74b9847b4fa89ce729d.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# #1 —运算符`==`和===有什么区别？

> 良好的 Javascript 实践不鼓励使用`==`操作符来减少类型转换导致的错误。现代林挺工具通常会标记出`==`的任何用法。因此，这个问题测试考生对 Javascript 的实际知识和经验

两个运算符都比较它们的两个操作数，并返回一个布尔结果

严格相等操作符`===`要求其操作数类型相同，否则返回`false`，而`==`操作符可能会在比较结果值之前尝试类型转换。

`===`认为`null`和`undefined`不同，而`==`认为相同

示例代码:

```
/* Equality */
1 == "1"           // true
1 == "00001"       // true
1 == "  00001   "  // true
null == undefined  // true

/* Strict equality */
1 === "1"          // false
null == undefined  // false 
```

参考资料:

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Strict _ equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality)

# #2 —什么时候使用`const`、`let`和`var`？

> 这个问题不仅测试候选人对新结构的熟悉程度，还验证候选人是否区分常数和正态变量。

`var`是 Javascript 中声明变量的最古老方式。函数中用`var`声明的变量具有该函数的作用域。如果在任何函数之外声明，它具有全局范围。使用`var`声明的变量在任何代码被执行之前*被创建，这个过程被称为提升，初始值被设置为`undefined`。使用`var`重新声明变量不会触发错误或重置其值，除非执行另一个赋值*

```
'use strict';
function foo() {
  function bar() {
    var y = 2;
    console.log(x); // undefined (x is hoisted, carrying "undefined")
    console.log(y); // 2 (`y` is in scope)
  }
  bar();
  var x = 1;        // x is initialized
  console.log(x);   // 1 (`x` is in scope)
  console.log(y);   // ReferenceError in strict mode, `y` is scoped to `bar`
}

foo();
```

`let`是声明变量的更新和首选方式。用`let`声明的变量具有块作用域(对同一个块和任何嵌套的作用域可见)，并且只有在其声明被执行*后才可访问* —相关概念:时间死区(TDZ)。在同一个块或函数中用`let`重新声明变量会导致语法错误

```
/* block scope variable */
let x = 1;
if (x === 1) {
  let x = 2;       // OK, redeclare in a different block

  console.log(x);  // expected output: 2
}
console.log(x);   // expected output: 1
let x = 10;        // syntax error

/* TDZ example */
{
  // TDZ starts at beginning of scope
  const func = () => console.log(letVar); // OK

  // Within the TDZ letVar access throws `ReferenceError`

  let letVar = 3; // End of TDZ (for letVar)
  func();         // Called outside TDZ!
}
```

`const`在`var`之后`let`之前引入，用于声明一个值不能改变的常量。因此`const`声明需要一个初始化器给变量分配一个常量值。变量的范围可以是全局的，也可以是块范围的。重新声明`const`变量导致语法错误。一个常见的惯例是用大写字母表示常量变量

```
const MY_CONSTANT = 111;

/** Errors:
MY_CONSTANT= 20;   // TypeError: Assignment to constant variable.
const MY_CONSTANT= 20;
let MY_CONSTANT= 20;
var MY_CONSTANT= 20;
*/

if (true) {
  let MY_CONSTANT = 20; // OK, different block scope
  console.log("my favorite number is " + MY_CONSTANT);  // 20
}

console.log("my favorite number is " + MY_CONSTANT);    // 111
```

参考资料:

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)

# # 3—如何创建新对象？

> 尽管不是面向对象的语言，object 还是经常出现在 Javascript 代码中。因此，知道如何用属性和方法创建对象是必须的。

在 Javascript 中创建对象最简单的方法是使用对象初始化器语法:一个由零对或多对属性名和对象的相关值组成的逗号分隔的列表，用花括号`{}`括起来。

```
const emptyObject = {}

const objectWithProperty = { 
   a: 1, 
   b: 'b', 
   c: true, 
   d: { nested: 'property'} 
}

const a = 1, b = 'b', c = true, d = { nested: 'property'}
const anotherObjectWithProperty = { a, b, c, d }

// Computed property names
const prop = 'foo';
const computedObjectProperty = {
  [prop]: 'hey',
  ['b' + 'ar']: 'there',
};
```

`new Object()`或`Object.create()`也可以用来创建一个新对象

```
const newObject = new Object();
newObject.a = 1;
newObject.b = 'b'

const anotherObject = Object.create(null);
```

参考资料:

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Object _ initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)

# **# 4——如何用计算面积的方法创建一个新的 5x5 正方形对象？**

> 这类似于问题 3，我们想测试候选人创造物体的能力。此外，它还测试考生的`this`知识和声明对象功能的不同方式

在版本 1 和版本 2 中，有两种有效的方法来声明下面显示的方法。

第三个版本是一个陷阱，因为 arrow 函数捕获封闭上下文的`this`的方式。使用`.call`或`.bind`将箭头功能绑定到对象不起作用。

```
// version 1
const square1 = { 
  side: 5,
  area: function () {
    return this.side * this.side;
  }
}
square1.area();  // 25

// version 2
const square2 = { 
  side: 5,
  area() {
    return this.side * this.side
  }
}
square2.area();  // 25

// version 3: warning: this with arrow function
const square3 = { 
  side: 5,
  area: () => this.side * this.side
}
square3.area();  // NaN - why? 
```

参考资料:

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Object _ initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)

# #5 —你用承诺(或可观察到的)做什么？

> 异步执行非常普遍。编写前端程序时很少不进行一些网络调用，或者设置超时或间隔。承诺的知识(或者如果你使用 Angular 或 RxJs 的话，是可观察的)是必不可少的。

Promise(或 Observable)是一种流行的异步 Javascript 编程方式。它允许开发人员编写代码来:

*   触发异步执行
*   然后，当它成功完成时，或者出错时，或者不管怎样，处理结果。

Promise(或 Observable)允许链接调用和处理程序。这提供了一种强大而直观的方式来对多个异步执行进行编程并处理它们的结果。

```
// Promise
const hello = fetch('https://echook.azurewebsites.net/echo')
  .then(resp => resp.text())
  .then(text => JSON.parse(text))   // or  resp.json() instead of text()
  .then(console.log)

// Angular's Observable
this.httpClient.get<string>('https://echook.azurewebsites.net/echo')
   .subscribe(resp => {
      console.log(resp.body)
    });
}
```

参考资料:

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
*   [https://angular.io/guide/observables-in-angular](https://angular.io/guide/observables-in-angular)

如果你喜欢这篇文章，请[关注我](https://medium.com/@geraldnguyen)获取更多优质内容。

谢谢你。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。****

****对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。**