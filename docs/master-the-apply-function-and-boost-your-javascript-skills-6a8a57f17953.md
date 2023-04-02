# 掌握 apply 函数并提高您的 JavaScript 技能

> 原文：<https://javascript.plainenglish.io/master-the-apply-function-and-boost-your-javascript-skills-6a8a57f17953?source=collection_archive---------10----------------------->

![](img/6447055ce2d8142244c3dec24893d75b.png)

[https://unsplash.com/photos/BfrQnKBulYQ](https://unsplash.com/photos/BfrQnKBulYQ)

## 如何在 JavaScript 中使用`apply`函数:示例和常见陷阱

`apply`函数是 JavaScript 中一个强大的工具，它允许您使用指定的上下文和一组参数调用指定的函数，这在许多情况下都很有用，比如当您想要将一组参数传递给不接受直接参数的函数时。但是，理解和正确使用可能会很困难。在这篇文章中，我们将仔细研究并提供如何在您的 JavaScript 代码中使用它的示例，最终，您将对`apply`函数有一个很好的理解，并知道何时以及如何有效地使用它，让我们来看看吧！

让我们从语法开始:

```
func.apply(thisArg, argsArray)
```

显然在这段代码中，`func`是一个函数

## JavaScript 中的`apply`函数是什么？

`apply`函数是 JavaScript 中所有`function`对象都有的函数。`apply`函数接受**两个**参数:

1.  一个上下文 *thisArg* (可以是一个对象或者`null`)
2.  参数数组 *argsArray* (可以是数组或者`null`)。

`apply`函数使用提供的上下文和参数调用指定的函数，然后返回该函数返回的值。

以下是如何使用`apply`函数在特定上下文中调用函数的示例:

```
function greet(greeting, punctuation) {
  return greeting + ' ' + this.name + punctuation;
}

var person = {
  name: 'John Doe'
};

// Invoke the `greet` function using `person` as the context
var message = greet.apply(person, ['Hello', '!']);

console.log(message); // 'Hello John Doe!'
```

在这个例子中，`greet`函数接受一个问候和一个标点符号作为参数，并使用上下文中指定对象的名称来创建一个问候消息。`apply`函数用于调用`greet`函数，使用`person`对象作为上下文，并将参数`'Hello'`和`'!'`作为数组传递。

使用`apply`函数的另一种方法是将一组参数传递给不接受直接参数的函数:

```
function sum() {
  return Array.prototype.reduce.call(arguments, function(a, b) {
    return a + b;
  });
}

var numbers = [1, 2, 3, 4, 5];

// Invoke the `sum` function using `numbers` as the arguments
var total = sum.apply(null, numbers);

console.log(total); // 15 
```

在这个例子中，`sum`函数使用数组的`reduce`函数对传递给该函数的所有参数求和。然而，`sum`函数不接受直接参数，所以`apply`函数用于将数字数组作为参数传递给`sum`函数。这允许使用`sum`函数对数组元素求和，而不必直接将它们作为参数传递。

## 另外两种方式

还有其他方法可以使用`apply`功能，让我们来看看。
首先是使用 apply()进行 f **函数借用**，下面是一个例子

```
// object definition
const airplane = {
  brand: "Airbus",
  model: "A380-800",
  lengthinMeters: "72",
  description() {
    return `The ${this.name} of ${this.model} is approximately ${this.lengthinMeters} meters in length.`;
  },
};

// object definition
const car = {
  brand: "Ford",  
  model: "Tourneo Courier",
  lengthinMeters: "4",
};

// car is borrowing description() method from airplane using apply() 
let result = airplane.description.apply(car);

console.log(result); 

//Output:
//The Tourneo Courier of Ford is approximately 4 meters in length. 
```

在上面的代码中，我们借助 apply()方法借用了`car`对象中的`airplane`对象方法。

第二个是**将它与内置函数**一起使用，比如`Math`它不是一个函数对象，但它是一个内置对象，具有数学常数和函数的属性和方法:

```
const numbers = [1, 25, 12, 32, 7];

const max = Math.max.apply(null, numbers);

console.log(max);
// expected output: 32

const min = Math.min.apply(null, numbers);

console.log(min);
// expected output: 1
```

使用`apply`函数的另一种方法是用一个**p end 两个数组**。看看这段代码:

```
let brand1 = ["BMW", "Audi", "Volvo"];
let brand2 = ["Toyota", "Ford"];

// appending two arrays color1 and color2
brand1.push.apply(brand1, brand2);

console.log(brand1);

//Output:
//[ 'BMW', 'Audi', 'Volvo', 'Toyota', 'Ford' ]
```

现在让我们来看看什么时候使用 apply()比较合适，根本不需要。

## 在 JavaScript 中何时以及如何使用`apply`函数

如前所述，`apply`功能可能难以理解和正确使用。困难的原因之一是不总是清楚什么时候使用应用功能，什么时候使用不同的方法。

让我们举一个例子，你根本不需要使用应用功能。

例如，在许多情况下，您希望使用`apply`函数向函数传递一组参数，您可以简单地使用 JavaScript `spread operator` ( `...`)来代替。

以下是如何使用`spread operator`而不是`apply`函数将数组元素作为参数传递给函数的示例:

```
 function sum(a, b, c, d, e) {
  return a + b + c + d + e;
}

var numbers = [1, 2, 3, 4, 5];

// Invoke the `sum` function using the `spread operator` to pass the elements of `numbers` as arguments
var total = sum(...numbers);

console.log(total); // 15
```

在这个例子中，`sum`函数接受五个参数，它们对应于`numbers`数组的元素。我们没有使用`apply`函数来传递数组作为参数，而是在调用`sum`函数时，在`numbers`数组之前使用了`spread operator` ( `...`)。这扩展了数组的元素，并将它们作为单独的参数传递给`sum`函数，这样我们就可以在不使用`apply`函数的情况下获得相同的结果。

在某些情况下，不使用 apply 更正确，因为其他函数更快、更有效。例如，在大型阵列上，`spread operator`要快得多

```
//Create an array of ten thousand random numbers
function randomArray() {
  var array = [];
  for (var i = 0; i < 100000; i++) {
    array.push(Math.floor(Math.random() * 100000));
  }
  return array;
}

//sum takes an indefinite number of arguments and returns their sum
function sum() {
  var total = 0;
  for (var i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

var tenkNumbers = randomArray(); 

console.time('apply');
var totalApply = sum.apply(null, tenkNumbers);
console.log(totalApply);
console.timeEnd('apply');
// 4997699420
// apply: 5.138ms

console.time('...');
var totalSpread = sum(...tenkNumbers);
console.log(totalSpread);
console.timeEnd('...');
// 4997699420
// ...: 0.684ms
```

如您所见，`spread operator`比`apply`功能快 5 倍多(*0.684 毫秒对 5.138 毫秒*)，因此尽管它在两种情况下都能工作，但最好使用扩展功能。时刻关注性能！

## …最后但同样重要的是

如果你熟悉`call()`函数，理解`apply()`函数会更容易，因为它们几乎是相同的，除了`call()`接受一个参数列表，而`apply()`接受一个参数数组。

```
//apply
func.apply(this, ['drive', 'car']) 
//call 
func.call(this, 'drive', 'car')
```

## 结论

总之，`apply`函数在 JavaScript 中很有用，但是很难理解何时以及如何正确使用`apply`函数，所以理解它的操作并知道何时可以使用不同的方法是很重要的。我希望这篇文章让您对 apply 函数有了基本的了解，并帮助您在 JavaScript 项目中正确使用它。

让我知道你的想法，如果你喜欢，也可以在推特或 LinkedIn 上关注我！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**