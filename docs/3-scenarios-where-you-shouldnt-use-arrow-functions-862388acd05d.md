# 不应该使用箭头函数的 3 种情况

> 原文：<https://javascript.plainenglish.io/3-scenarios-where-you-shouldnt-use-arrow-functions-862388acd05d?source=collection_archive---------5----------------------->

![](img/76eb77c2aaca80917a26c81e75bacb8e.png)

Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

与普通函数(用`function`关键字声明)相比，箭头函数有许多不同之处，包括:

*   箭头函数没有自己的`[this](https://www.javascripttutorial.net/javascript-this/)`值
*   它没有`arguments`的对象。
*   它没有`[[construct]]`内部插槽。

这里有 3 种不应该使用箭头函数的情况。

# 1.在对象上定义方法

在 JavaScript 中，方法是存储在对象的属性中的函数。当调用该方法时，`this`成为该方法所属的对象。

## 1a。对象文字

因为 arrow 函数有一个简短的语法，所以把它用于方法定义是很有吸引力的。让我们试一试:

`calculate.sum`用箭头函数定义方法。但是在调用时`calculate.sum()`抛出一个`TypeError`，因为`this.array`被赋值为`undefined`。
在`calculate`对象上调用方法`sum()`时，上下文保持`window`。这是因为 arrow 函数用`window`对象在词汇上绑定了上下文。
执行`this.array`相当于`window.array`，也就是`undefined`。

解决方案是使用函数表达式或[速记语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)进行方法定义(ECMAScript 6 中提供)。在这种情况下，`this`由调用决定，而不是由封闭上下文决定。我们来看看修复版:

因为`sum`是一个常规函数，调用`calculate.sum()`时的`this`是`calculate`对象。`this.array`是数组引用，因此元素之和计算正确:`6`。

## 1b。对象原型

当在一个`prototype`对象上定义方法时，同样的规则也适用。
没有使用箭头函数来定义`sayCatName`方法，这带来了不正确的上下文`window`:

使用*老校*函数表达式:

# 2.具有动态上下文的回调函数

`this`在 JavaScript 中是一个强大的特性。它允许根据调用函数的方式改变上下文。上下文通常是发生调用的目标对象，这使得代码更加自然。它像是在说“这个物体发生了一些事情”。

然而，arrow 函数将上下文静态地绑定在声明上，不可能使其成为动态的。这是奖牌的另一面，在这种情况下词汇`this`是不必要的。

将事件侦听器附加到 DOM 元素是客户端编程中的一项常见任务。一个事件触发以`this`为目标元素的处理函数。动态上下文的便捷使用。

下面的示例尝试对这样的处理程序使用箭头函数:

`this`是在全局上下文中定义的箭头函数中的`window`。当点击事件发生时，浏览器试图用`button`上下文调用处理函数，但是箭头函数不会改变其预定义的上下文。

`this.innerHTML`相当于`window.innerHTML`，没有意义。

您必须应用一个函数表达式，它允许根据目标元素改变`this`:

```
const button = document.getElementById('myButton');
button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```

当用户点击按钮时，处理函数中的`this`为`button`。因此`this.innerHTML = 'Clicked button'`正确修改按钮文本以反映点击状态。

# 3.调用构造函数

`this`在构造调用中是新创建的对象。执行`new MyFunction()`时，构造函数`MyFunction`的上下文是一个新对象:`this instanceof MyFunction === true`。

请注意，箭头函数不能用作构造函数。JavaScript 通过抛出一个异常隐式地阻止了这样做。

总之`this`是从封闭上下文中设置的，不是新创建的对象。换句话说，一个箭头函数构造函数调用是没有意义的，而且是不明确的。

让我们看看，如果尝试:

```
const Message = (text) => {
  this.text = text;
};
// Throws "TypeError: Message is not a constructor"
const helloMessage = new Message('Hello World!');
```

执行`new Message('Hello World!')`，其中`Message`是一个箭头函数，JavaScript 抛出一个`Message`不能作为构造函数的`TypeError`。

我认为在这种情况下，ECMAScript 6 失败并显示详细的错误消息是一种有效的做法。与*相反，静默失败*特定于以前的 JavaScript 版本。

上面的例子是使用[函数表达式](https://developer.mozilla.org/en/docs/web/JavaScript/Reference/Operators/function)修复的，这是创建构造函数的正确方法(包括[函数声明](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/function)):

```
const Message = function(text) {
  this.text = text;
};
const helloMessage = new Message('Hello World!');
console.log(helloMessage.text); // => 'Hello World!'
```

# 语法太短

arrow 函数有一个很好的特性，如果函数体只有一个语句，它可以省略参数圆括号`()`，块花括号`{}`和`return`。这有助于编写非常短的函数。

我的大学编程教授给学生布置了一个有趣的任务:用 C 语言写出计算字符串长度的最短函数。这是学习和探索一门新语言的好方法。

然而，在现实世界的应用程序中，许多开发人员都会阅读这些代码。最短的语法并不总是适合帮助你的同事即时理解函数。

在某种程度上，压缩的函数变得难以阅读，所以尽量不要激动。让我们看一个例子:

```
const multiply = (a, b) => b === undefined ? b => a * b : a * b;
const double = multiply(2);
double(3);      // => 6
multiply(2, 3); // => 6
```

`multiply`返回两个数字的乘法结果或一个与第一个参数相关联的闭包，用于后面的乘法。

该功能运行良好，看起来很短。但是第一眼看上去可能很难理解它的作用。

为了提高可读性，可以从 arrow 函数中恢复可选的花括号和`return`语句，或者使用常规函数:

```
function multiply(a, b) {
  if (b === undefined) {
    return function(b) {
      return a * b;
    }
  }
  return a * b;
}
const double = multiply(2);
double(3);      // => 6
multiply(2, 3); // => 6
```

在简短和冗长之间找到一个平衡点是很好的，这样可以让你的 JavaScript 简单明了。

# 结论

毫无疑问，箭头功能是一个很好的补充。当正确使用时，它在以前你不得不使用`.bind()`或试图抓住上下文的地方带来了简单性。这也使得代码更轻。

某些情况下的优势会带来其他情况下的劣势。需要动态上下文时不能使用箭头函数:定义方法，用构造函数创建对象，处理事件时从`this`获取目标。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*