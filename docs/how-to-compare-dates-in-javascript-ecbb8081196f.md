# 如何在 JavaScript 中比较日期对象

> 原文：<https://javascript.plainenglish.io/how-to-compare-dates-in-javascript-ecbb8081196f?source=collection_archive---------2----------------------->

## 在这篇博客中，我们讨论并比较了 JavaScript 中比较日期的 5 种方法。

在用 JavaScript 构建应用程序时，我们经常要处理日期。比较日期可能会很乏味，因为要考虑很多事情，比如日、月、年、时间等等。

JavaScript 有内置的 date 对象，允许我们比较两个日期。让我们讨论如何比较我们拥有的两个日期，看看它是如何工作的。注意，这个博客只适用于 JavaScript 的原生日期对象。

![](img/be266be8e7d3825b2ccd81bf3ebb1acb.png)

## 1)直接比较两个日期对象:

我们可以像处理其他变量一样，使用比较运算符`<`或`>`来比较两个日期。这是解决这个问题最直接的方法。

```
d1 = new Date() // today's date
d2 = new Date(2021, 02, 05) // previous dateif (d1 > d2) {
  console.log('d1 is greater than d2')
}
else {
  console.log('d2 is greater than d1')
}// result: d1 is greater than d2
```

> 注意:注意`===`和`==`不能与 d1 和 d2 一起使用。因为日期对象是对象。我们不能直接比较两个对象，因为对象是引用类型。但是我们可以比较一下性质。

```
d1 = new Date(2021, 02, 05)
d2 = new Date(2021, 02, 05)d1 === d2 // false
d1 == d2 // false
```

## 2)使用。getTime()

使用`.getTime()`是比较两个日期是否相等的方法之一。

`.getTime()`返回给定日期的数值，即自**1970 年 1 月 1 日 00:00:00 UTC** 起经过的毫秒数。

```
d1 = new Date(2021, 02, 05)
d2 = new Date(2021, 02, 05)if (d1.getTime() === d2.getTime()) {
  console.log('Two dates are equal')
}
else {
  console.log('Two dates are NOT equal')
}// Result: Two dates are equal
```

注意，它也适用于`<`和`>`比较运算符。

```
d1 = new Date('2022, 05, 10') 
d2 = new Date('2022, 05, 05') if (d1.getTime() > d2.getTime()) {   
  console.log('d1 is ahead than d2') } 
else {   
  console.log('d2 is ahead than d1') 
}  
// Result: d1 is ahead than d2
```

## 3)使用。toString():

我们可以使用`.toString()`将日期对象转换为字符串，然后使用`==`或`===`进行比较。

```
d1 = new Date('2022, 05, 05') 
d2 = new Date('2022, 05, 05') if (d1.toString() === d2.toString()) 
{   
   console.log('Two dates are equal') 
} 
else 
{   
   console.log('Two dates are NOT equal') 
} 
// Result: Two dates are equal
```

> ***注意:*** 因为我们要将一个对象转换成一个字符串，所以比较操作符如`<`和`>`在这里不能正常工作。

```
d1 = new Date('2022, 05, 10') 
d2 = new Date('2022, 05, 15') if (d1.toString() > d2.toString()) {   
console.log('d1 is ahead than d2') 
} else {   
console.log('d2 is ahead than d1') 
} // Result: d1 is ahead than d2  
// > and < do not work when we are using .toString() method.
```

## 4)使用。值为:

`valueOf()`方法返回指定对象的原始值。这个方法也像`.getTime()`一样返回经过的毫秒数。下面是我们如何使用它。

```
d1 = new Date(2021, 02, 05)
d2 = new Date(2021, 02, 05)if (d1.valueOf() === d2.valueOf()) {
  console.log('Two dates are equal')
}
else {
  console.log('Two dates are NOT equal')
}// Result: Two dates are equal
```

这对于`<`和`>`也同样适用。所以这是一个优势。

```
d1 = new Date('2022, 05, 10') 
d2 = new Date('2022, 05, 15') if (d1.valueOf() > d2.valueOf()) {   
 console.log('d1 is ahead than d2') 
} else {   
 console.log('d2 is ahead than d1') 
}  
// Result: d2 is ahead than d1
```

## 5)减去两个日期:

减去两个日期，检查结果是否为 0。如果为 0，则两个日期相等。减去`a - b`得到两个日期之间的差值，单位为毫秒。

```
d1 = new Date()
d2 = new Date()if ((d2 - d1) === 0) {
  console.log('Two dates are EQUAL')
}
else {
  console.log('Two dates are NOT equal')
}// Result: Two dates are EQUAL
```

我们可以通过将两个日期相减，检查结果是 ***正*** 还是 ***负来比较两个日期。***

```
d1 = new Date('2022, 05, 10')
d2 = new Date('2022, 05, 15')if (d1 - d2 > 0) {
  console.log('d1 is ahead than d2')
}
else {
  console.log('d2 is ahead than d1')
}// Result: d2 is ahead than d1
```

# JavaScript 中的仅日期比较:

有时，我们可能不想考虑时间部分，但希望比较对象的日期部分。

我们可能需要分别借助`.getFullYear()`、`.getMonth()`和`.getDate()`来提取年、月和日。这些是内置方法，是 JavaScript date 对象的一部分。

```
function isDateEqual(date1, date2) {
  if (
    date1.getFullYear() === date2.getFullYear() &&
    date1.getMonth() === date2.getMonth() &&
    date1.getDate() === date2.getDate()
  ) {
    return "Two dates are Equal";
  } else {
    return "Two dates are not equal";
  }
}const date1 = new Date("2021, 05, 05");
const date2 = new Date("2021, 05, 06");console.log(isDateEqual(date1, date2));// Result: Two dates are Equal
```

# 参考资料:

*   [https://www.scaler.com/topics/compare-dates-in-javascript/](https://www.scaler.com/topics/compare-dates-in-javascript/)
*   [https://livecodestream . dev/post/everything-you-should-know-about-comparing-dates-in-JavaScript/](https://livecodestream.dev/post/everything-you-should-know-about-comparing-dates-in-javascript/)
*   [https://stack overflow . com/questions/26531212/comparising-dates-in-JavaScript-and-time zones](https://stackoverflow.com/questions/26531212/comparing-dates-in-javascript-and-timezones)
*   [JavaScript 中的日期](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
*   [object . prototype . tostring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
*   [object . prototype . value of()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

# 结论:

我们找到了。我们学习了 5 种比较日期对象的方法。如果你知道任何其他方法，请在下面评论。

感谢您的阅读🙃

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***