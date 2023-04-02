# 更简洁的 JavaScript:更简洁、可读性更强的代码的技巧和技术

> 原文：<https://javascript.plainenglish.io/cleaner-javascript-tips-and-techniques-for-more-concise-readable-code-93598fa6c85e?source=collection_archive---------13----------------------->

使用这些提示来缩短你的代码

编写更简洁的 JavaScript 代码通常会缩短代码长度，这有几个好处。首先，较短的代码通常更容易阅读和理解，这可以使它更易于维护，更不容易出错。这在团队环境中尤其重要，在团队环境中，许多人可能在同一个代码库上工作。其次，代码越短，效率越高，无论是从占用的空间还是执行的时间来看都是如此。最后，较短的代码可以更灵活，适应性更强，因为它不太可能被不必要的细节拖累，并且可以更容易地修改以满足不断变化的需求。通过努力编写更短的代码，您可以提高代码库的质量和可维护性。让我们开始吧！

![](img/4a8267e1d3a5f542fb08f776592c6102.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## **箭头功能**

箭头函数是用 JavaScript 编写函数的一种更简洁的语法。它们是匿名函数，通常用来代替常规函数，以此来编写更短、更简洁的代码。箭头函数可以在许多与常规函数相同的地方使用，包括作为对象、回调中的方法，甚至作为生成器。arrow 函数的一些关键特性包括:它们没有自己的 this 值，不能用作构造函数，并且没有原型属性。此外，箭头函数可以用“词法”风格编写，这意味着它们继承了封闭上下文的 this 值。这使得它们对于编写回调函数特别有用。例如，您可以像这样使用箭头函数:

```
const numbers = [1, 2, 3, 4, 5];

// Previously we had to write functions like this
const squareNumbers = numbers.map(function(x) {
    return x * x;
});
// we begin by changing the function keyword to an 
// arrow by removing the function keyword and adding 
// the "fat arrow" syntax with equals and greater than
const squareNumbers = numbers.map((x) => {
    return x * x;
});
// we can remove the parentheses around x if there is only one parameter
const squareNumbers = numbers.map(x => {
    return x * x;
});
// we can remove the curly braces and the return keyword if the function 
// body is a single expression
const squareNumbers = numbers.map(x => x * x);
// We can also access any item in the array by adding the 
// index at the end of the statement
const squareNumbers = numbers.map(x => x * x)[0];

// All of these functions are equivalent and will return the same result
console.log(squareNumbers); // [1, 4, 9, 16, 25]
```

总的来说，箭头函数是用 JavaScript 编写简洁、优雅代码的强大而有用的工具。

## 解构

在 JavaScript 中，析构是一种允许您轻松地从数组或对象中提取值并将它们赋给变量的特性。这是一种从数组或对象的属性创建变量的便捷方式，可以帮助您编写更简洁、可读性更好的代码。例如，假设您有一个包含两个元素的数组，您想从这些元素中创建两个变量。你可以这样使用析构:

```
const numbers = [1, 2];
const [first, second] = numbers;

console.log(first);  // Output: 1
console.log(second); // Output: 2
```

这也可以通过对象来实现。例如，假设您有一个具有两个属性的对象，您想从这些属性中创建两个变量。你可以这样使用析构:

```
const person = {
  name: "John",
  age: 30
};
const { name, age } = person;

console.log(name);  // Output: "John"
console.log(age);   // Output: 30
```

析构是 JavaScript 的一个强大而方便的特性，它可以让你的代码更易读、更容易编写。

## 属性值速记

属性值速记是 JavaScript 的一个特性，它允许您从一组与对象属性同名的变量中创建一个对象。当您想从一组变量中创建一个对象时，这是一种编写更简洁、可读性更强的代码的便捷方式。

例如，假设您有两个变量，`name`和`age`，您想从这些变量中创建一个对象。您可以这样使用属性值简写:

```
const name = "John";
const age = 30;
const person = { name, age };

console.log(person);  // Output: { name: "John", age: 30 }
```

如您所见，这比另一种方法更简洁，可读性更强，那就是将对象写成这样:

```
const person = {
  name: name,
  age: age
};
```

属性值速记在处理对象时非常有用，可以帮助您编写更简洁、可读性更好的代码。这是一个在处理大型复杂数据结构时特别有用的特性。

## 模板字符串

在 JavaScript 中，模板字符串是创建字符串文字的一种方式，它可以跨越多行文本并包含嵌入式表达式。这些字符串由反斜杠(`)分隔，而不是 JavaScript 中常用的单引号或双引号。

下面是一个模板字符串的示例:

```
const name = "John Doe";
const message = `Hello, ${name}!`;
```

如您所见，模板字符串包含了`${name}`占位符，当字符串被求值时，它将被替换为`name`变量的值。这允许您创建动态的字符串，并且可以包含变量和表达式的值。

模板字符串还支持字符串插值，这允许您将表达式的结果直接包含在字符串中。例如:

```
const x = 10;
const y = 20;
const message = `The sum of x and y is ${x + y}.`;
```

在这种情况下，`${x + y}`占位符将被替换为`x + y`表达式的结果，即 30。这是在字符串中包含复杂表达式的一种便捷方式，无需将多个字符串连接在一起。

如您所见，该字符串包含换行符和多行文本，但它仍然包含在一个字符串中。在计算字符串时，将保留换行符和空白，从而允许您创建可读性更强、更易于格式化的字符串。这是一个多行消息的示例:

```
const message = `This is a
multiline template string.
It can span multiple lines
and include line breaks.`;
```

总的来说，模板字符串为在 JavaScript 中创建字符串提供了一种更易读、更方便的方式，尤其是在处理复杂的表达式或多行字符串时。

## 传播算子

JavaScript 中的 spread 操作符允许您将一个数组或对象展开成它的单个元素。例如，如果您有一个名为`myArray`的数组，并且您想要将它的元素添加到另一个名为`newArray`的数组中，那么您可以使用 spread 运算符来实现，如下所示:

```
const myArray = [1, 2, 3];
const newArray = [4, 5, 6];

newArray = [...myArray, ...newArray];
```

这会将`myArray`的元素添加到`newArray`的开头，导致`newArray`包含元素`[1, 2, 3, 4, 5, 6]`。“扩展”操作符也可以用于以类似的方式扩展对象。

下面是一个使用 spread 运算符将两个对象合并在一起的示例:

```
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };

const mergedObj = { ...obj1, ...obj2 };
```

这将导致`mergedObj`包含`obj1`和`obj2`的键和值，因此它将具有属性`a`、`b`、`c`和`d`。

以下是使用 spread 运算符可以做的一些其他事情:

您可以使用它来创建数组或对象的浅表副本。这意味着您可以创建一个包含与原始数组或对象相同的元素或属性的新数组或对象，但是对新数组或对象的更改不会影响原始数组或对象。例如:

```
const myArray = [1, 2, 3];
const copyOfArray = [...myArray];

// changes to copyOfArray won't affect myArray
copyOfArray.push(4);
```

您可以使用 spread 运算符将数组元素作为单独的参数传递给函数。这通常比将整个数组作为单个参数传递更方便。例如:

```
const myArray = [1, 2, 3];

// instead of calling the function like this:
myFunction(myArray);

// you can use the spread operator to call it like this:
myFunction(...myArray);
```

您可以使用 spread 运算符将字符串转换为字符数组。例如:

```
const myString = 'hello';
const myArray = [...myString];

// myArray will be ['h', 'e', 'l', 'l', 'o']
```

这些只是使用 spread 操作符可以做的几个例子。这是一个非常通用的工具，可以使你的代码更加简洁，可读性更好。

我们已经讨论了现代 JavaScript 的几个特性，这些特性可以使您的代码更加简洁，可读性更好。这些特性包括箭头函数，它为定义函数提供了紧凑的语法；析构，允许你从数组或对象中提取值，并将它们赋给变量；属性值速记，允许您通过指定对象的属性和值来创建对象，而无需重复属性名；模板字符串，它使得生成包含动态表达式的字符串文字更加容易；以及 spread 运算符，它允许您将数组或对象展开为单个元素。编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***