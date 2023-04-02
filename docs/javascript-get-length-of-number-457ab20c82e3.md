# 如何在 JavaScript 中获得一个数字的长度

> 原文：<https://javascript.plainenglish.io/javascript-get-length-of-number-457ab20c82e3?source=collection_archive---------8----------------------->

## 学习在 JavaScript 中轻松计算数字位数的多种方法。

![](img/d76a77dda5f50cc797f97753bf68b7a0.png)

# 1.字符串表示的长度属性

要得到一个数字的长度，调用数字上的`toString()`方法将其转换为一个字符串，然后访问字符串的`length`属性，即`num.toString().length`。

```
const num1 = 12345;
const num2 = 524;console.log(num1.toString().length); // 5
console.log(num2.toString().length); // 3
```

我们对数字调用`toString()`方法来获得它的字符串表示。

```
const num1 = 12345;
const num2 = 524;console.log(num1.toString()); // '12345'
console.log(num2.toString()); // '524'
```

`String`对象有一个长度属性，它返回字符串中的字符数(UTF-16 代码单位)。我们用这个来得到数字的长度。

## 获取浮动的长度

对于浮点数，当访问浮点数的字符串表示的`length`属性时，将包括小数点。

```
const float1 = 123.45; // 5 digits
const float2 = 524.1; // 4 digitsconsole.log(float1.toString().length); // 6
console.log(float2.toString().length); // 5
```

为了避免这种情况并获得浮点中的实际位数，只需从`length`中减去 1。

```
const float1 = 123.45; // 5 digits
const float2 = 524.1; // 4 digitsconsole.log(float1.toString().length - 1); // 5
console.log(float2.toString().length - 1); // 4
```

# 2.Math.ceil()和 Math.log10()方法

我们也可以用纯数学的方法得到一个数的长度:

```
function getNumberLength(num) {
  return Math.ceil(Math.log10(num + 1));
}const num1 = 12345;
const num2 = 524;console.log(getNumberLength(num1)); // 5
console.log(getNumberLength(num2)); // 3
```

`Math.log10()`方法返回一个数以 10 为底的对数。

```
console.log(Math.log10(12345)); // 4.091491094267951
```

而`Math.ceil()`方法将一个数向上舍入到下一个最大的整数。

```
console.log(Math.ceil(4.091491094267951)); // 5
```

不幸的是，这种方法对 floats 无效。它只返回小数点前的位数。

```
function getNumberLength(num) {
  return Math.ceil(Math.log10(num + 1));
}const float1 = 123.45; // 5 digits
const float2 = 524.1; // 4 digitsconsole.log(getNumberLength(float1)); // 3
console.log(getNumberLength(float2)); // 3
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/a4c453)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。