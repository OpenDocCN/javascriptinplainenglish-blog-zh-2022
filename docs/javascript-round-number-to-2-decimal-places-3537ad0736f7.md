# 如何在 JavaScript 中将数字四舍五入到小数点后两位

> 原文：<https://javascript.plainenglish.io/javascript-round-number-to-2-decimal-places-3537ad0736f7?source=collection_archive---------7----------------------->

![](img/b6495e642fd809a3caf22287735e36d9.png)

在 JavaScript 中，要将一个数字四舍五入到小数点后两位，请对该数字调用`toFixed()`方法，即`num.toFixed(2)`。`toFixed()`将数字四舍五入并格式化到小数点后两位。

例如:

Java Script 语言

```
const num = 5.3281;

const result = num.toFixed(2);
console.log(result); // 5.33

const num2 = 3.1417
const result2 = num2.toFixed(2);
console.log(result2); // 3.14
```

`[toFixed()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)`方法接受一个数字`F`，并返回一个数字的字符串表示，小数点后有`F`位数。`F`这里由传递给`toFixed()`的第一个参数决定，即`fractionDigits`参数。

```
const num = 5.3281;

console.log(num.toFixed(0)); // 5

console.log(num.toFixed(1)); // 5.3

console.log(num.toFixed(2)); // 5.33

console.log(num.toFixed(3)); // 5.328

console.log(num.toFixed(4)); // 5.3281

console.log(num.toFixed(5)); // 5.32810
```

# 将`toFixed()`的结果解析为数字

记住，`toFixed()`返回一个**字符串**表示:

```
const num = 5.3281;

const result = num.toFixed(2);

console.log(result); // 5.33
console.log(typeof result); // string
```

但是我们总是可以用`[Number()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)`构造函数将结果转换成一个数字:

```
const num = 5.3281;

const result = Number(num.toFixed(2));
console.log(result); // 5.33
console.log(typeof result); // number
```

如果字符串有尾随零，它们将在转换中被删除:

```
const num = 9.999999;

const strResult = num.toFixed(2);
const result = Number(strResult);
console.log(strResult); //10.00
console.log(result); // 10
```

小数点后的尾随零不会改变数字的值，因此`10.00`与`10`或`10.00000000`相同

```
console.log(10.00 === 10); // true

console.log(10.00000000 == 10); // true
```

# 将十进制字符串四舍五入到小数点后两位

有时输入可能存储为字符串。在这种情况下，我们首先需要用`[parseFloat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)`函数将数字转换成浮点数，然后用`toFixed()`将其四舍五入到两位小数。

例如:

```
const numStr = '17.23593';

// 👇 convert string to float with parseFloat()
const num = parseFloat(numStr);
const result = num.toFixed(2); // 17.24
console.log(result);
```

不是所有的十进制数都可以用二进制精确表示，所以 JavaScript 的浮点数系统存在一些舍入误差。例如:

```
console.log(44.85 * 0.1); // 4.485

console.log(45.85 * 0.1); // 4.585

console.log(46.85 * 0.1); // 4.6850000000000005 (?)
```

在本例中，`46.85 x 0.1`等于`4.6850000000000005`，因为`46.85`不能用二进制浮点格式准确表示。

```
console.log((1.415).toFixed(2)); // 1.42

console.log((1.215).toFixed(2)); // 1.22

console.log((1.015).toFixed(2)); // 1.01 (?)
```

和第一个一样，这里的`1.015`被四舍五入到小数点后两位作为`1.01`而不是`1.02`，因为`1.015`在二进制数字系统中也无法准确表示。

这种缺陷最流行的例子之一是经典的`0.1 + 0.2`:

```
console.log(0.1 + 0.2 === 0.3); // false

console.log(0.1 + 0.2); // 0.30000000000000004
```

你可以在我们的[疯狂 JS 书籍](https://codingbeautydev.com/crazy-js-book)中找到这个和更多其他有趣的 JavaScript 怪癖。

*原载于*[*【codingbeautydev.com】*](https://cbdev.link/96e6d7)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。