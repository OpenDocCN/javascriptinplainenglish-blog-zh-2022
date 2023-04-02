# 正则函数与阿罗函数的比较研究

> 原文：<https://javascript.plainenglish.io/regular-function-vs-arrow-function-a-comparative-study-abfa22391131?source=collection_archive---------11----------------------->

## 知道普通函数和箭头函数的区别。

![](img/0afd2affe73487931c9ae687b9136a81.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

```
// Regular Function 
const greet = function (name) {
  return `Hello ${name}`;
}// Arrow Function with one parameter
const greet = name => {
  return `Hello ${name}!`;
}// Arrow function with two parameters
const greet = (name, age) => {
  return `Hello, my name is ${name} and I am ${age} !`;
}
```

# 争论

在一个常规函数中，您可以使用一个特殊的关键字`arguments`访问该函数接收到的参数列表:

```
function myFunction() {
  console.log(arguments);
}
myFunction('a', 'b'); // logs { 0: 'a', 1: 'b', length: 2 }
```

在箭头函数中，`arguments`特殊关键字**不存在。**它会抛出一个错误:`arguments is not defined`

# 隐性回报

有了 arrow 函数，就不一定需要在末尾放一个 return 语句。

如果你的函数只包含一个表达式你不需要写花括号或者 return 语句，这个函数会**隐式**返回表达式的结果:

```
const increment = num => num + 1;
increment(41); // returns 42
```

对于正则表达式，如果`return`语句丢失，函数将返回`undefined`:

```
function myFunction() {
  'Hello';
}myFunction();  // returns undefined
```

# 这

箭头功能没有自己的`this`。如果你不知道这是什么关键字，我来解释一下。

在函数内部，`this`是一个对象，指的是执行上下文。这个对象的值是动态的，取决于你如何调用函数表达式。

在一个箭头函数`this` **内部，总是**等于**外部环境的值，**它不定义自己的执行上下文。

# 新的

用关键字`new`你可以创建一个对象的实例。例如，如果我们创建一个 Plane 对象，我们可以调用 Plane 类型的一个名为“redPlane”的新 Plane 实例。

```
function Dog(breed) {
  this.breed = breed;
}const shibaInu = new Dog('Shiba inu')
```

但是箭头函数不能作为构造函数，所以不能用`new`调用。如果您尝试，您将收到以下错误:`TypeError: Car is not a constructor`

```
function Dog(color) {
  this.breed = breed;
}const shibaInu = new Dog('Shiba inu'); // TypeError: Dog is not a constructor
```

# 重复的命名参数

在常规函数中，可以多次使用相同的参数名称(如果不在严格模式下) :

```
function add(x, x){ return x + x }
```

使用箭头功能，完全禁止**使用**，并会抛出错误:

`SyntaxError: duplicate argument names not allowed in this context`

什么时候你会选择使用其中一个？我觉得只是喜好问题，但是如果你觉得我错了就告诉我！

我真的很想知道你用什么语法来定义你的函数。你更喜欢箭头函数还是常规函数？

谢谢你，祝你编码愉快。👋

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*