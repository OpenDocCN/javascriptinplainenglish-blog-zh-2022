# JavaScript 中的严格模式是什么——综合指南

> 原文：<https://javascript.plainenglish.io/what-is-strict-mode-in-javascript-a-comprehensive-guide-b3fcd9daa220?source=collection_archive---------6----------------------->

## JavaScript 中关于**严格模式的一些有趣的事情。**

![](img/dbdd296c925c9c4c315809576b98272b.png)

Image from [unsplash](https://unsplash.com/) @ [kingschurchinternational](https://unsplash.com/@kingschurchinternational)

*面试时，面试官会问，****JavaScript 中的严格模式是什么？*** *作为被采访者，你的回答是什么？
你团队中的初级开发人员请教* ***严格模式*** *。作为一个资深开发者，你打算怎么解释？*

*严格模式使得安全程序的编写没有错误。*

# 怎么…🤔

*   **严格模式**通过将一些 JavaScript 静默错误改为抛出错误来消除它们。
*   修复了使 JavaScript 引擎难以执行优化的错误。严格模式代码有时可以比非严格模式的相同代码运行得更快。
*   禁止某些可能在 ECMAScript 未来版本中定义的语法。

# 如何使用严格模式？

调用严格模式的语法是`'use strict';`(或`"use strict";`)。
在 JavaScript 中有两种方式调用严格模式:

1.  在全局范围内调用整个脚本。
2.  为单个函数调用。

## 在全局范围内调用整个脚本

```
'use strict'; // Apply strict mode to the entire scriptfullName = 'John Doe';const userObj = {
   name: this.fullName,
   sayMySelf: function() {
      age = 30;
      console.log(`I am ${this.name} and I am a ${age} years old!`);
   }
}userObj.sayMySelf();
```

在上面的程序中，**严格模式**将应用于整个脚本，并将为变量`fullName`和`age.`给出`not defined`错误

## 为单个函数调用

```
fullName = 'John Doe';const userObj = {
   name: this.fullName,
   sayMySelf: function() {
      'use strict'; // Apply to the sayMySelf function
      age = 30;
      console.log(`I am ${this.name} and I am a ${age} years old!`);
   }
}userObj.sayMySelf();
```

在上述程序中，严格模式仅适用于`sayMySelf`功能，并给出`age is not defined`错误。

## 在严格模式下使用未声明的变量

```
'use strict';const user = {
  name: 'John Doe',
  sayName: function () {
     console.log(fullName)
  }
}user.sayName();
```

在上面的代码示例中，在`sayName`函数中使用了一个未声明的变量`fullName`。用**严格模式**上面的代码会抛出一个 ***引用错误指示******没有定义*** 。

然而，如果我们给一个名字(在我们的例子中是`fullName`)赋值，而这个名字没有用`let`、`const`或`var`声明，会发生什么呢？
如果我们用**严格模式**这样做，它会给出与上面相同的错误。

但是如果这是没有**严格模式的**，它最终会创建一个新的全局变量。无论我们的代码中函数和块的嵌套有多深，它都将是全局的，这几乎肯定不是您想要的，容易出错，并且是使用**严格模式**的最好理由之一。查看下面的代码示例，了解更多信息。

```
const objectOne = {
  name: 'John Doe',
  setName: function () {
    fullName = 'John Doe';
  }
}const objectTwo = {
  name: 'John Doe',
  sayName: function () {
    console.log(fullName); // Will print John Doe
  }
}objectOne.setName();
objectTwo.sayName();console.log(fullName); // Will print John Doe
```

## 在严格模式下使用`delete`关键字

在**严格模式**下删除变量或函数是不允许的，会抛出错误。

```
'use strict';const x = 3;
function y() {};// These will cause errors
delete x;
delete y;
```

让我给你看一个关于`delete`操作符的有趣的事情。暂时忘记**严格模式**，如果我们在 web 浏览器中运行下面的代码，输出会是什么？

```
fullName = 'John Doe';
var x = 3;delete fullName;
delete x;console.log(window.x); // this will log 3 to the browser console
console.log(window.fullName); // this will log undefined
```

在上面的例子中，`fullName`也是在全局范围内创建的，就像用`var`关键字定义的变量一样。*但是与适当的* `*var*` *声明定义的属性不同，这些属性可以用* `*delete*` *操作符删除。*

**关于** `**delete**` **操作员的附加知识:**

```
const cities = ["Colombo", "London", "New Delhi"];
delete cities[2];console.log(2 in cities); // true or false ?
console.log(cities.length); // 3 or 2 ?
```

## 在严格模式下使用 eval()

`eval()`允许在被调用的范围内创建变量和函数。此外，`eval()`允许改变变量值或与`eval()`共享相同局部范围的函数行为。

```
var x = 1;
eval('var x = 2; var y = 4;');function fn() {
  console.log(1);
}
eval('function fn() { console.log(2) };');
fn();
```

**严格模式**不允许在被调用的范围内使用`eval()`创建变量，也不允许改变变量值或与`eval()`共享相同局部范围的函数的行为。

此外，**严格模式**通过有效地将**“eval”**变成保留字，使`eval()`更像操作符。我们不允许用新值覆盖`eval()`功能。并且我们不允许用名称 **"eval"** 声明一个**变量**、**函数**、**函数参数**或 **catch 块参数**。

## 在严格模式下使用 with 运算符

`with`语句运行代码块，就好像指定对象的属性是该代码范围内的变量一样。不明白？
看一下代码示例。

```
var x = Math.round(9.75);
var pi = Math.PI;
```

我们可以使用`with`如下编写上面的代码示例。

```
with (Math) {
  var x = round(9.75);
  var pi = PI;
}
```

**严格模式**不允许使用`with`运算符，在非严格模式下应被视为已弃用。尽可能避免使用它。使用`with`的 JavaScript 代码很难优化，并且很可能比没有使用`with`语句的代码运行得慢得多。

## 在严格模式下使用它

对于非严格模式下的函数调用，调用上下文(`this`)是全局对象。然而，在**严格模式**中，调用上下文是`undefined`。请注意，使用 arrow 语法定义的函数行为不同。它们总是继承在它们被定义的地方有效的`this`值。

当使用`call()`或`apply()`调用函数时，`this`值就是作为第一个参数传递给`call()`或`apply()`的值。
在**非严格模式**中，`null`和`undefined`值被替换为全局对象，非对象值被转换为对象。

如果您需要更多的代码示例说明，请阅读我的 [**上一篇文章**](/arrow-functions-vs-regular-functions-in-js-fa1a1f235c86) 。

此外，**严格模式**限制遵循 JavaScript 中的。

*   不可写属性的赋值和在不可扩展对象上创建新属性的尝试抛出一个**类型错误**。在**非严格模式下，**这些尝试会无声无息地失败。
*   对象文本用相同的名称定义两个或多个属性是语法错误。在**非严格模式**下，没有错误发生。
*   函数声明中有两个或更多同名的参数是语法错误。
*   不允许八进制整数文字(以 0 开头，后面没有 x)。在**非严格模式**中，一些实现允许八进制文字。
*   检查调用堆栈的能力受到限制。`arguments.caller`和`arguments.callee`都在**严格模式**函数内抛出一个**类型错误**。严格模式函数也有调用者和参数属性，当被读取时抛出**类型错误**。(有些实现在非严格函数上定义了这些非标准属性。)

为了创作这篇文章，我参考了[大卫·弗拉纳根](https://medium.com/u/70b3d287f497?source=post_page-----b3fcd9daa220--------------------------------)的 [**JavaScript 权威指南**](https://www.amazon.com/JavaScript-Definitive-Most-Used-Programming-Language/dp/1491952024) 书。

感谢阅读。😍

## 你是 JavaScript 爱好者吗？

请阅读下面我写的文章，了解一些关于 JavaScript 的令人兴奋的事情。

*   [*箭头函数与 JavaScript 中的常规函数——综合指南*](/arrow-functions-vs-regular-functions-in-js-fa1a1f235c86)
*   [*JavaScript 吊装—综合指南*](/javascript-hoisting-a-comprehensive-guide-89211c219d45)
*   [*JavaScript 中的本地存储与会话存储—综合指南*](/local-storagevs-session-storage-in-javascript-a-comprehensive-guide-df887398e69)

希望你在阅读这篇文章时能学到一些新东西。请 [***关注我***](https://medium.com/@sudarshanadayananda) *以后阅读这类文章。干杯！*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW)**并加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***