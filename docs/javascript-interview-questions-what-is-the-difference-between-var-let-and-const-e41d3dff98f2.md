# var，let & const: JavaScript 面试问题#1 (ES6)有什么区别

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-what-is-the-difference-between-var-let-and-const-e41d3dff98f2?source=collection_archive---------2----------------------->

## 理解 JavaScript 中 var、let 和 const 的区别。

![](img/015ffcaf09d46afb06b7a4068ce45f69.png)

# var，let & const 有什么区别

在 ECMAScript 6 中，JavaScript 开发人员的生活中有了一个新的变量定义。

在 ES6 之前，JavaScript 变量声明为:

```
**var = 'value'**
```

但是现在在 ES6 之后，我们可以用两种不同的方式声明变量。

这两种方式是:

*   **让**
*   **常量**

在本文中，我们将讨论 **let** 和 **const 的区别。**

## **让**

let 用于声明变量。

使用 **let** 声明的变量是**块范围的。**这意味着变量只能在特定的块中访问。

```
let language = "Javascript"
```

如果该变量是在函数内部定义的，那么它只能在函数内部被访问。

## Let vs Var

let 和 var 实际上是不同的东西，我们可以定义三个不同的东西。

**让是**

*   块范围
*   let 不允许重新声明变量
*   提升不会发生在左侧

**var 为**

*   函数范围
*   var 允许重新声明变量
*   提升发生在 var

## let 是块范围的

下面的例子:

```
function test() {
  var x = "x";
  let y = "y";

  console.log(x, y); // x y

  {
    var moo = "Mooo"
    let baz = "Bazz";
    console.log(moo, baz); // Mooo Bazz
  }

  console.log(moo); // Mooo
  console.log(baz); // ReferenceError
}

test();
```

如您所见，块中声明的 baz 在这里无法到达。

这导致了之前 for 循环的一些问题，如下例所示:

```
for (var i = 0; i < 3; i++) {
  var j = i * 2;
}
console.log(i); // 3
console.log(j); // 4

for (let k = 0; k < 3; k++) {
  let l = k * 2;
}
console.log(typeof k); // undefined
console.log(typeof l); // undefined
```

试图在这里做 **console.log(k)** 或 **console.log(l)** 会抛出一个 ReferenceError。

现在对同一个变量使用不同的循环变得容易多了，没有任何问题。

## let 不允许重新声明变量

用 var 声明的变量可以重新声明:

```
var a = 3;
var a = 5;
```

运行时不会出现任何问题:

但是如果我们尝试用 let 做同样的事情:

```
let a = 5;
let a = 3; // error
```

在不同的作用域中重新声明 var 的值也会改变外部作用域中 var 的变量。

```
var a = 5;
console.log(a); // 5
{
    var a = 3;
    console.log(a); // 3
}
console.log(a); // 3
```

在不同的范围内重新声明 let 不会改变该值。但是不要忘记，在同一个块中，不能用 let 多次重新声明这个值。

```
let a = 5;
console.log(a); // 5
{
    let a = 3;
    console.log(a); // 3
}
console.log(a); // 5
```

## 不允许吊装

用 var 声明的变量允许提升到脚本范围的顶部。

例如:

```
console.log(a);
var a; // undefined
```

但是如果我们想用**做同样的事情，让:**

```
console.log(a);
let a; // Uncaught ReferenceError: a is not defined
```

**让不允许吊装。**

## 常数

在 JavaScript 中， **const** 用于声明常量变量。

例如:

```
const language = "Javascript" 
```

一旦你声明了一个常量值，你就不能改变**常量**变量。

仅此而已:)

*如果你觉得这篇文章很有帮助，你* [***可以通过使用我的推荐链接注册一个***](https://medium.com/@melihyumak) **[***中级会员来访问类似的文章***](https://melihyumak.medium.com/membership) *。***

***跟我上*** [**推特**](https://twitter.com/hadnazzar)

[![](img/c012fae801a3ab846a63dc560d09ff17.png)](https://www.youtube.com/c/TechnologyandSoftware)

Subscribe for more on [**Youtube**](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)

# 编码快乐！

梅利赫

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*