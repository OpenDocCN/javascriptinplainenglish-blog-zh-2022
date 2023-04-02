# JavaScript Set 对象—存储唯一值

> 原文：<https://javascript.plainenglish.io/javascript-set-object-to-store-unique-values-e330ab7a886c?source=collection_archive---------15----------------------->

![](img/3b2f8e008ee9ab537429e1339d9b200b.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的`Set`是一种特殊类型的对象，它允许我们存储唯一的值。它适用于原始和非原始数据类型的值。

在存储大量数据时，我们总是可以选择数组。但是如果我们想要存储唯一的值，与数组相比，`Set`是一个更好的选择。虽然在数组中，我们可以手动过滤掉所有重复的值，或者我们可以在添加到集合时检查该值是否已经存在。

```
const set = new Set();
```

`Set()`构造函数创建一个新的`Set`对象。这个构造函数还接受一个可选参数，该参数必须是[可迭代的](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)。如果我们传递任何参数，它将过滤掉所有不重复的值，并将它们添加到新的`Set`中。但如果我们一个都不通过，`Set`就空了。

内置可迭代的例子有数组、映射、字符串、生成器等。

```
const set1 = new Set();
console.log(set1); // Set(0) {size: 0}

const set2 = new Set([2, 'x', 5, true, 2, 'x', true, 6]);
console.log(set2); // Set(5) {2, 'x', 5, true, 6}

// checking for String
const set3 = new Set('world');
console.log(set3); // Set(5) {'w', 'o', 'r', 'l', 'd'}

// String with duplicate characters
const set4 = new Set('madam');
console.log(set4); // Set(3) {'m', 'a', 'd'}
```

# 实用方法和属性

`Set`对象提供了几个助手方法，我们可以用它们来添加/删除值，或者检查是否有值存在，等等。让我们把他们都找出来。

## add()方法

该方法将值添加到`Set`对象的末尾。如果该值已经存在于`Set`中，它不会添加它。这个方法返回更新后的`Set`对象。

```
const set = new Set();
set.add(10); // Set(1) {10}
set.add('Hello'); // Set(2) {10, 'Hello'}
set.add(10); // Set(2) {10, 'Hello'}
set.add(20); // Set(3) {10, 'Hello', 20}
set.add('Hello'); // Set(3) {10, 'Hello', 20}
```

当我们添加非原始值时，`Set`通过它们的引用而不是值来测试它们的唯一性。让我们看一个例子。

```
const ob1 = { x: 2 };
const ob2 = ob1;
const ob3 = { x: 2 };

const set = new Set();
set.add(ob1); // Set(1) {{...}}
set.add(ob2); // Set(1) {{...}}
set.add(ob3); // Set(2) {{...}, {...}}
```

这里`ob1`和`ob2`引用同一个对象，所以`Set`将`ob2`视为重复，没有添加。另一方面，`ob3`与`ob1`和`ob2`具有相同的值，但是它引用了不同的对象，因此`Set`将其视为唯一的并添加了它。

> **注意:**`Set`认为所有的`NaN`值都一样，尽管`NaN !== NaN`。

`add()`方法是可链接的。

```
const set = new Set();
set.add(8).add(null).add("Hello").add(NaN).add();
// Set(5) {8, null, 'Hello', NaN, undefined}

set.add(NaN).add(undefined).add(null).add(false);
// Set(6) {8, null, 'Hello', NaN, undefined, false}
```

## delete()方法

这个方法从`Set`中删除值。它将值作为我们想要从`Set`中移除的参数。如果传递的值存在于`Set`中，`delete()`将其移除并返回`true`，否则返回`false`。

```
const set = new Set();
set.add(8); // Set(1) {8}
set.add('Hello'); // Set(2) {8, 'Hello'}
set.delete(8); // true
set.delete('world'); // false
console.log(set); // Set(1) {'Hello'}
```

## has()方法

该方法检查值是否出现在`Set`中。如果该值存在，则返回`true`，否则返回`false`。

```
const set = new Set();
set.add('Hello'); // Set(1) {'Hello'}
set.add(8); // Set(2) {'Hello', 8}
set.delete('Hello'); // Set(1) {8}
console.log(set.has(8)); // true
console.log(set.has('Hello')); // false
```

## clear()方法

这个方法删除了所有出现在`Set`对象中的值。

```
const set = new Set([2, "x", true, 10]);
set.clear();
console.log(set); // Set(0) {size: 0}
```

## 大小属性

该属性返回出现在`Set`对象中的值的数量。

```
const set = new Set([2, "x", 2, 5]);
console.log(set.size); // 3
```

## forEach()方法()

该方法遍历`Set`值，并为每个值调用提供的回调函数。

```
const set = new Set();
set.add(5).add(8).add(2); // Set(3) {5, 8, 2}
set.forEach((value) => {
  console.log(value);
});
/*
5
8
2
*/
```

我们也可以使用`for…of`循环来迭代`Set`。

```
const set = new Set();
set.add(5).add(8).add(2); // Set(3) {5, 8, 2}
for (const value of set) {
  console.log(value);
}
/*
5
8
2
*/
```

# 将集合转换为数组

有许多方法可以将一个`Set`转换成一个数组，但是我们将只讨论最简单和最方便的方法。我们知道，`Set`是可迭代的，我们可以使用 spread 操作符或`Array.from()`方法从`Set`创建一个数组。

```
const set = new Set();
set.add(5).add(10).add('Hello'); // Set(3) {5, 10, 'Hello'}
const arr1 = [...set];
const arr2 = Array.from(set);
console.log(arr1); // [5, 10, 'Hello']
console.log(arr2); // [5, 10, 'Hello']
```

# 使用 Set 从数组中删除重复项

要使用`Set`从数组中删除重复项，首先，我们可以从数组中创建一个`Set`对象，然后将`Set`转换回数组。

```
const arr = [10, 5, 20, 10, 6, 5, 8, 5, 20];
const set = new Set(arr);
const newArr = [...set];
console.log(newArr); // [10, 5, 20, 6, 8]

// shorthand
console.log([...new Set(arr)]);
```

# 你可能也喜欢

*   [JavaScript 中的地图，当它是比对象更好的选择时](https://jscurious.com/map-in-javascript-and-how-it-is-better-than-object/)
*   [用 JavaScript 中的 HTMLAudioElement API 播放音频](https://jscurious.com/play-audio-with-htmlaudioelement-api-in-javascript/)
*   [JavaScript 中的 URLSearchParams API](https://jscurious.com/the-urlsearchparams-api/)
*   [JavaScript 中的 Object.defineProperty()方法](https://jscurious.com/object-defineproperty-method-in-javascript/)
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [JavaScript 中承诺的简要指南](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20+ JavaScript 速记编码技巧和窍门](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的时间:)*
***阿米塔夫·米什拉***

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。*