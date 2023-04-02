# 如何在 JavaScript 中将秒转换成小时和分钟

> 原文：<https://javascript.plainenglish.io/javascript-convert-seconds-to-minutes-and-hours-5e4ce5920522?source=collection_archive---------10----------------------->

![](img/a2c779094cd30e5b945e28dc5d9495f3.png)

要在 JavaScript 中将秒转换为小时和分钟:

1.  用秒除以 60 得到总分钟数。输出中的余数将是秒。
2.  用总分钟数除以 60 得到小时数。结果中的整数将是小时，余数将是输出中的分钟。

例如:

```
function toHoursAndMinutes(totalSeconds) {
  const totalMinutes = Math.floor(totalSeconds / 60);

  const seconds = totalSeconds % 60;
  const hours = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60;
  return { h: hours, m: minutes, s: seconds };
}

// { h: 0, m: 1, s: 0 }
console.log(toHoursAndMinutes(60));

// { h: 0, m: 16, s: 40 }
console.log(toHoursAndMinutes(1000));

// { h: 1, m: 10, s: 50 }
console.log(toHoursAndMinutes(4250));
```

我们创建了一个可重用的函数，它使用总秒数，并返回一个包含单独的小时、分钟和秒钟值的对象。

首先，我们将总秒数除以 60，得到总分钟数。

```
console.log(60 / 60); // 1

console.log(1000 / 60); // 16.666666666666668

console.log(4250 / 60); // 70.83333333333333
```

除法的结果是一个小数，所以我们使用`Math.floor()`函数来得到结果的整数。

`[Math.floor()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)`返回小于或等于指定数字的最大整数。

```
console.log(Math.floor(10.95)); // 10
console.log(Math.floor(10)); // 10
console.log(Math.floor(10.05)); // 10
```

在这之后，我们使用模运算符(`%`)来获得结果中秒的除法余数。

```
console.log(60 % 60); // 0

console.log(1000 % 60); // 40

console.log(4250 % 60); // 50
```

**提示:**如果秒不应该在结果中，跳过这一步。

我们都知道 60 秒构成一分钟，60 分钟构成一小时。在获得总分钟数之后，我们做一些类似于我们刚才对总秒数值所做的事情:我们将总分钟数除以 60 以获得小时数，并使用模运算符获得除法的余数，这将是输出中的分钟数。

获得所有值后，我们返回一个具有`h`、`m`和`s`属性的对象，分别包含小时、分钟和秒。

```
return { h: hours, m: minutes, s: seconds };
```

# 将秒转换为`HH:mm:ss`

您可能希望结果是一个类似于`HH:mm:ss`格式的时间字符串，而不是一个对象，其中每个值由冒号分隔，并且字符串中至少有两位数字。下面是我们如何产生这样一个时间字符串。

```
function toTimeString(totalSeconds) {
  const totalMs = totalSeconds * 1000;
  const result = new Date(totalMs).toISOString().slice(11, 19);

  return result;
}

console.log(toTimeString(60)); // 00:01:00

console.log(toTimeString(1000)); // 00:16:40

console.log(toTimeString(4250)); // 01:10:50
```

首先，我们将秒转换为毫秒，将其传递给`[Date()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)`构造函数，并创建一个新的`Date`对象。

`[Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString)`[toISOString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString)`方法以 ISO 8601 格式返回日期的字符串表示，即`YYYY-MM-DDTHH:mm:ss.sssZ`

```
const totalMs = 60000;

// 1970-01-01T00:01:00.000Z
console.log(new Date(totalMs).toISOString());
```

你可以看到`toISOString()`为我们做了转换。我们只需要一种从 ISO 字符串中提取`HH:mm:ss`的方法。

`[String slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)`方法返回指定的开始和结束索引之间的字符串部分，分别作为第一个和第二个参数传递。

`HH:mm:ss`从字符串的索引 11 开始，到索引 18 结束。所以为了提取它，我们传递给`slice()`或`substring()`的值将是`11`和`19`。

**提示:** `19`因为`slice()`从结果子串中排除了结束索引处的字符。

```
// 00:01:00
console.log('1970-01-01T00:01:00.000Z'.slice(11, 19));
```

要从结果中排除秒，我们需要将结束索引减少 3，以排除冒号和秒的数字。

```
// 00:01
console.log('1970-01-01T00:01:00.000Z'.slice(11, 16));
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/f1c2bb)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***