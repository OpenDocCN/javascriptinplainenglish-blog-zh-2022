# 如何在 JavaScript 中将分钟转换成小时和分钟

> 原文：<https://javascript.plainenglish.io/javascript-convert-minutes-to-hours-and-minutes-d20b92d83856?source=collection_archive---------5----------------------->

## 了解如何在 JavaScript 中轻松地将单独的总分钟数转换为完整的小时数和剩余分钟数。

![](img/af075fad737cf4ef5ad1b7001b19cd2d.png)

要在 JavaScript 中将分钟转换为小时和分钟，请将分钟除以 60。小时是结果的整数，分钟是除法的余数。

例如:

```
function toHoursAndMinutes(totalMinutes) {
  const hours = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60; return { hours, minutes };
}// { hours: 1, minutes: 40 }
console.log(toHoursAndMinutes(100));// { hours: 1, minutes: 0 }
console.log(toHoursAndMinutes(60));// { hours: 2, minutes: 10 }
console.log(toHoursAndMinutes(130));
```

我们创建了一个可重用的函数，它获取总的分钟数，并返回一个包含单独的小时和分钟值的对象。

首先，我们将总分钟数除以 60，得到完整的小时数。除法将产生一个浮点数，所以我们使用`Math.floor()`函数来得到商的整数。

[Math.floor()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) 返回小于或等于指定数字的最大整数。

```
console.log(Math.floor(10.95)); // 10
console.log(Math.floor(10)); // 10
console.log(Math.floor(10.05)); // 10
```

之后，我们使用模操作符(`%`)得到总分钟数除以 60 的余数。结果是剩余的分钟数。

```
console.log(100 % 60); // 40
console.log(60 % 60); // 0
console.log(130 % 60); // 10
```

我们返回一个具有`hour`和`minute`属性的对象，它们分别具有完整小时和剩余分钟的值。

# 返回带有时间格式的字符串

我们也可以返回其他格式的结果，这取决于我们的用例。例如，我们可以将小时和分钟作为带有时间格式的字符串返回。

```
function toHoursAndMinutes(totalMinutes) {
  const hours = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60; return `${padToTwoDigits(hours)}:${padToTwoDigits(minutes)}`;
}function padToTwoDigits(num) {
  return num.toString().padStart(2, '0');
}console.log(toHoursAndMinutes(100)); // 01:40
console.log(toHoursAndMinutes(60)); // 01:00
console.log(toHoursAndMinutes(130)); // 02:10
```

这里我们使用`padStart()`方法，如果小时和分钟值是个位数，就用零填充它们。

[String padStart()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart) 方法根据需要多次用另一个字符串填充当前字符串，直到结果字符串达到指定长度。

```
const str1 = '7';
const str2 = 'abc';console.log(str1.padStart(3, '0')); // 007
console.log(str2.padStart(5, '*')); // **abc
console.log(str2.padStart(3, '*')); // abc
```

我们返回的字符串是时间格式`HH:mm`，但是您可以使用另一种格式来适应您的用例。

# 返回带有缩写标签的字符串

在下面的例子中，我们返回一个字符串，其中包含用`h`表示的整小时，以及用`m`表示的剩余分钟(如果存在的话):

```
function toHoursAndMinutes(totalMinutes) {
  const hours = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60; return `${hours}h${minutes > 0 ? ` ${minutes}m` : ''}`;
}console.log(toHoursAndMinutes(100)); // 1h 40m
console.log(toHoursAndMinutes(60)); // 1h
console.log(toHoursAndMinutes(130)); // 2h 10m
```

我们使用三元运算符来确保剩余分钟数大于零，然后用缩写显示它们。

*更新于:*[*codingbeautydev.com*](https://cbdev.link/af3979)

您可以在哪里找到我们:

🌐[网站](https://cbdev.link/b621b9) |🌟[推特](https://twitter.com/CodingBeautyDev) |🌟[脸书](http://facebook.com/CodingBeautyDev)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。