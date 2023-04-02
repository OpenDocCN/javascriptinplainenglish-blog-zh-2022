# JavaScript 生成器函数—完整指南

> 原文：<https://javascript.plainenglish.io/javascript-generator-functions-a-complete-guide-52c2ead5af23?source=collection_archive---------5----------------------->

![](img/d16a3ae7d5c2a7f9b25af62b18a04492.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 生成器是一种特殊类型的函数，它允许您暂停函数的执行，稍后再回来继续执行。

我们可以用关键字`function`后跟一个星号(`function*`)定义一个生成器函数。目前，箭头函数没有这样的选项来创建生成器函数。

生成器函数提供了一个名为`yield`的强大关键字，它暂停函数执行并返回`yield`表达式值。

```
function* generatorFn() {
    console.log('start');
    yield 1;
    console.log('After yield 1');
    yield 2;
    console.log('end');
}
```

当我们调用生成器函数时，它不会立即执行。相反，它返回一个包含三个实用方法的`[Generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)`对象。

*   下一个()
*   return()
*   投掷()

# next()方法

当我们调用`next()`方法时，生成器函数一直执行到下一个`yield`表达式。该方法返回一个对象，该对象包含一个保存生成值的`value`属性和一个保存布尔值的`done`属性，该布尔值指示函数是否已完成执行。

```
function* generatorFn() {
    console.log('start');
    yield 10;
    console.log('After yield 10');
    console.log('X', yield 20);
    console.log('end');
}

const gen = generatorFn();
console.log(gen.next());
console.log(gen.next());
console.log(gen.next());
```

输出:

```
start
{ value: 10, done: false }
After yield 10
{ value: 20, done: false }
X undefined
end
{ value: undefined, done: true }
```

**代码解释:** 第一个`next()`调用——函数将执行到第一个`yield`表达式`yield 10`。因此，将打印“start ”,并且由包含属性`value`为“10”和属性`done`为`false`的`yield 10`返回一个对象。

第二次`next()`调用–函数将从第二行(无`yield`表达式)开始执行，直到下一个`yield`表达式`yield 20`。记住，当执行在一行上暂停时，它只执行`yield`表达式，语句的其余部分将在下一个`next()`调用中执行。因此，在第二个`next()`调用中，只有`yield 20`会执行并暂停，rest 控制台语句将在下一次迭代中执行。

第三个`next()`调用–函数将从第四行开始执行，执行控制台语句并用`undefined`替换`yield 20`(因为我们在`next()`中没有传递任何参数)。稍后我们会详细了解)。由于没有更多的`yield`表达式，执行将继续到最后，并返回包含`value`的对象作为`undefined`和包含`done`的对象作为`true`。

一旦执行完成，调用`next()`将总是返回属性`value`为`undefined`和`done`为`true`的对象。

## 在生成器函数中放置 return 语句

如果我们在生成器函数中有一个`return`语句，那么`return`语句将完成执行，返回的对象将把`value`作为返回值，把`done`作为`true`。

```
function* generator() {
    yield 1;
    return 5;
}

const gen = generator();
console.log(gen.next());
// { value: 1, done: false }
console.log(gen.next());
// { value: 5, done: true }
```

如果我们将`return`语句放在任何`yield`表达式之前，那么`return`语句将结束执行，而`yield`表达式将被忽略。

```
function* generator() {
    yield 1;
    return 5;
    yield 10;
}

const gen = generator();
console.log(gen.next()); 
// { value: 1, done: false }
console.log(gen.next()); 
// { value: 5, done: true }
console.log(gen.next()); 
// { value: undefined, done: true }
```

## 在 next()方法中传递值

我们可以用一个参数调用`next()`方法，它将用参数值替换最后执行的`yield`表达式，在那里执行被暂停。

```
function* generator() {
    yield 10;
    const third = yield 20;
    yield third;
}

const gen = generator();
console.log(gen.next()); 
// { value: 10, done: false }
console.log(gen.next(55)); 
// { value: 20, done: false }
console.log(gen.next(99)); 
// { value: 99, done: false }
console.log(gen.next()); 
// { value: undefined, done: true }
```

这里，当第一个`next()`被调用时，`yield 10`被执行，执行在那里被暂停。

当调用`next(55)`时，它用“55”替换最后一个`yield`表达式，即`yield 10`(我们在这里不使用这个值，所以我们看不到区别)，然后执行`yield 20`，执行在那里暂停。

当`next(99)`被调用时，它将最后一个`yield`表达式即`yield 20`替换为“99”，并将值“99”赋给变量“third”。然后`yield third`执行并返回属性`value`为“99”的对象，并在那里暂停执行。

最后，当最后一个`next()`被调用时，最后一个`yield`之后的代码被执行，这里最后一个`yield`之后没有可用的代码，所以它简单地完成执行并返回带有`done`作为`true`的对象。

# return()方法

当我们调用`return()`方法时，它将在执行暂停的地方完成函数的执行。它将返回一个属性为`undefined`和`done`的对象。我们还可以在`return()`方法中传递一个值，该值将替换返回对象中的`value`属性。

```
function* generator() {
  console.log("start");
  yield 10;
  console.log("after yield 10");
  yield 20;
  console.log("end");
}

const gen = generator();
console.log(gen.next());
console.log(gen.return(55));
console.log(gen.next());
```

输出:

```
start
{ value: 10, done: false }
{ value: 55, done: true }
{ value: undefined, done: true }
```

# throw()方法

这个方法基本上在那里停止执行并抛出一个异常。这个方法不会像`next()`和`return()`那样返回任何对象。出于调试目的，我们可以将任何错误信息传递给该方法。

```
function* generator() {
  console.log("start");
  yield 10;
  console.log("after yield 10");
  yield 20;
  console.log("end");
}

const gen = generator();
console.log(gen.next());
console.log(gen.throw(new Error('Some error occured')));
console.log(gen.next());
```

输出:

```
start
{ value: 10, done: false }
Uncaught Error: Some error occured
```

# 作为迭代器的生成器对象

generator 对象是 [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol) ，所以我们可以很容易地遍历它并使用每个`yield`表达式返回的值。

```
function* generator() {
  yield 25;
  yield 45;
  yield 65;
}

// using for...of loop
for (let value of generator()) {
  console.log(value);
}
// 25
// 45
// 65

// Array.from()
console.log(Array.from(generator())); 
// [25, 45, 65]

// spread operator
console.log([...generator()]); 
// [25, 45, 65]
```

# 对 iterables 使用 yield*关键字

`yield*`关键字迭代[可迭代](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)操作数，并产生它返回的每个值。该关键字只能用于 iterables，否则会引发错误。

一些内置的可迭代对象是数组、映射、字符串、生成器等。

## 字符串和数组示例

```
function* generator() {
  yield 10;
  yield [20, 30];
  yield* [40, 50];
  yield 'html';
  yield* 'js';
}

const gen = generator();

console.log(gen.next().value); // 10
console.log(gen.next().value); // [20, 30]
console.log(gen.next().value); // 40
console.log(gen.next().value); // 50
console.log(gen.next().value); // html
console.log(gen.next().value); // j
console.log(gen.next().value); // s
```

## 发电机示例

```
// print a series of numbers like 1223334444...n(n times)

function* repeat(n) {
  let count = 1;
  while (count <= n) {
    yield n;
    count++;
  }
}

function* generateSequence(n) {
  let count = 1;
  while (count <= n) {
    yield* repeat(count);
    count++;
  }
}

const gen = generateSequence(3);
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
console.log(gen.next().value); // 3
console.log(gen.next().value); // 3
console.log(gen.next().value); // undefined
```

# 生成器函数的多个实例

我们可以创建生成器的多个实例，它们不会干扰彼此的执行并独立工作。让我们看一个例子。

```
function* generator() {
  yield 10;
  yield 20;
}

const gen1 = generator();
const gen2 = generator();

console.log(gen1.next()); 
// { value: 10, done: false }
console.log(gen1.next()); 
// { value: 20, done: false }
console.log(gen2.next());
// { value: 10, done: false }
console.log(gen1.next()); 
// { value: undefined, done: true }
console.log(gen2.next()); 
// { value: 20, done: false }
console.log(gen2.next()); 
// { value: undefined, done: true }
```

# 你可能也喜欢

*   [使用 JavaScript 中的通知 API 发送推送通知](https://jscurious.com/the-notification-api-in-javascript/)
*   [用 JavaScript 中的 HTMLAudioElement API 播放音频](https://jscurious.com/play-audio-with-htmlaudioelement-api-in-javascript/)
*   [JavaScript 中的地图，当它是比对象更好的选择时](https://jscurious.com/map-in-javascript-and-how-it-is-better-than-object/)
*   [JavaScript 中检查对象中是否存在键的不同方法](https://jscurious.com/different-ways-to-check-if-a-key-exists-in-an-object/)
*   [JavaScript 中承诺的简要指南](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript Object.is()方法检查两个值是否相等](https://jscurious.com/javascript-object-is-method/)
*   [CSS:is()和:where()伪类](https://jscurious.com/the-css-is-and-where-pseudo-classes/)
*   [JavaScript 获取 API 以发出 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20+ JavaScript 速记编码技巧和窍门](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的时间:)*
***阿米塔夫·米什拉***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***