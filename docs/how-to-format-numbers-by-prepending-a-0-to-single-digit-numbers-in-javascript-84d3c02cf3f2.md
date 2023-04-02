# 如何在 JavaScript 中通过在一位数前加一个 0 来格式化数字？

> 原文：<https://javascript.plainenglish.io/how-to-format-numbers-by-prepending-a-0-to-single-digit-numbers-in-javascript-84d3c02cf3f2?source=collection_archive---------7----------------------->

![](img/1e11742e2119f6ef2eebfc3d3bd7b435.png)

Photo by [Clément Falize](https://unsplash.com/@centelm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望通过在数字前假装零来格式化数字，直到它匹配给定的长度。

在本文中，我们将了解如何通过用前导零填充数字来格式化数字，直到它满足给定的长度。

# `Number.prototype.toLocaleString`

用前导零填充数字的一种方法是使用`toLocaleString`方法。

它让我们用前导零填充一个数字，直到它达到最小长度。

例如，我们可以写:

```
const formattedNumber = (2).toLocaleString('en-US', {
  minimumIntegerDigits: 2,
  useGrouping: false
})
console.log(formattedNumber)
```

用前导零填充数字 2 直到它变成两位数。

`minimumIntegerDigits`设置为 2，这样返回的数字字符串至少有 2 个字符长。

`useGrouping`设置为`false`删除给定区域的任何数字分组分隔符。

所以，`formattedNumber`就是`'02'`。

# 编写我们自己的函数

我们也可以编写自己的函数来填充一个数字字符串，直到它满足给定的长度。

例如，我们可以写:

```
function leftPad(number, targetLength) {
  let output = number.toString();
  while (output.length < targetLength) {
    output = '0' + output;
  }
  return output;
}const formattedNumber = leftPad(2, 2)
console.log(formattedNumber)
```

我们创建了`leftPad`函数，它将`number`作为参数进行格式化，将`targetLength`作为参数进行填充。

我们用`toString`方法将`number`转换成一个字符串，并将其赋给`output`。

然后我们使用一个`while`循环在`output`前面加上零，直到满足`targetLength`为止。

然后我们返回`output`字符串。

所以当我们用 2 和 2 调用`leftPad`时，我们得到`'02'`。

# `String.prototype.padStart`

另一种用零填充数字字符串直到给定长度的方法是使用 string `padStart`方法。

例如，我们可以写:

```
const formattedNumber = (2).toString().padStart(2, "0");
console.log(formattedNumber)
```

我们在 2 上调用`toString`将其转换成一个字符串。

然后我们用我们想要填充的长度和填充字符串的字符在它上面调用`padStart`。

`padStart`重复在字符串前面加上第二个参数中的字符，直到满足第一个参数中的长度。

因此，`formattedNumber`与其他例子相同。

# 结论

我们可以用 JavaScript 通过几个简单的方法或操作格式化带有前导零的数字，直到它满足给定的长度。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*