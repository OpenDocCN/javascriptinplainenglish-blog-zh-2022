# 如何在 JavaScript 中检查一个数字是否是完美的正方形

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-number-is-a-perfect-square-in-javascript-3eef757e37a4?source=collection_archive---------9----------------------->

## 毁灭 2022

![](img/85babf73fe93f968df4ed2713853f10c.png)

Image by [Samuele](https://medium.com/@el3um4s)

我的《毁灭 2022》的第二个问题与平方根有关。问题的[故事是关于立方体、正方形和对数字的热情。但长话短说，这是关于一个数字是否是一个完美的正方形。](https://www.codewars.com/kata/54c27a33fb7da0db0100040e)

这个问题非常简单，我的解决方案只需要几个步骤:

```
export default function isSquare(n: number): boolean {
  const square: number = n ** 0.5;
  const truncated: number = Math.trunc(square);

  return square == truncated;
}
```

在 JavaScript 中，它变成了:

```
const isSquare = function (n) {
  const square = n ** 0.5;
  const truncated = Math.trunc(square);

  return square == truncated;
};
```

换句话说，首先我计算这个数字的平方。为此，我使用指数操作符`**`设置`1/2`作为指数。或者，我可以使用 [Math.sqrt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/sqrt) 。

```
const square = n ** 0.5;
const square = Math.sqrt(n);
```

然后我必须弄清楚得到的数字是否是整数。我可以用两种方法做这件事。最长的方法是截断数字，并检查结果是否等于原始数字。

```
const truncated = Math.trunc(square);
const isInteger square == truncated;
```

最简单的方法是使用 [Number.isInteger()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger) 方法。

```
const isInteger = Number.isInteger(square);
```

最后，我还可以使用[余数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder) `%`运算符来检查被`1`除的余数是否返回`0`。

```
const isSquare = (n) => Math.sqrt(n) % 1 === 0;
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***