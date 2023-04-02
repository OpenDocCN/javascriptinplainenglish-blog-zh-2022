# JavaScript:检查一个数字是否是斐波纳契数的最有效方法

> 原文：<https://javascript.plainenglish.io/javascript-the-most-efficient-way-to-check-if-a-number-is-a-fibonacci-number-e513618a598d?source=collection_archive---------12----------------------->

## 毁灭 2022

## 利用比奈公式节省时间和资源

![](img/45af3ed228ebf8c774cbfa1a216c30c2.png)

圣诞节快到了，这个多灾多难的 2022 也接近尾声。我今天没有太多时间，所以我将解决一个与斐波那契数列和 JavaScript 相关的小问题。我需要一个有效的方法来检查一个数字是否属于斐波纳契数列。最好不必每次都重建数值序列。

# 斐波那契数

但是让我们从基础开始。首先，什么是斐波那契数列？它是一个整数序列，其中每个数字都是前两个数字的和，除了前两个数字，根据定义，它们是 0 和 1。

该系列的第一个元素是数字:

> 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233,

# 明显的解决方案

![](img/56cb7e319af9f1db455858c0c7b79bf9.png)

找出一个数是否属于该数列的最明显的解决方法是每次都计算数列本身，直到达到所寻找的数。这是一个函数示例:

```
const isFibonacci = (n) => {
  let a = 0;
  let b = 1;
  if (n == a || n == b) {
    return true;
  }

  let c = a + b;
  while (c <= n) {
    if (c === n) return true;
    a = b;
    b = c;
    c = a + b;
  }
  return false;
};
```

这种做法有什么问题？嗯，随着要检查的数量增加，所需的计算时间也会增加。这是一种可行的方法，但在现实世界中没有用。

# 更好的解决方案

![](img/91ae950d02b3a92c15e2224f9e284213.png)

为了解决这个问题，稍微研究一下斐波纳契数列的性质是很有用的。维基百科来帮忙了，并引用了雅克·菲利普·玛丽·比奈的话。比奈是法国数学家。在他的发现中，我们可以算出一个公式，它允许我们[计算斐波那契数列的第 n 个数字](https://en.wikipedia.org/wiki/Jacques_Philippe_Marie_Binet):

> f(n)=(φ^n-(1-φ)^n)/sqrt(5)

其中`F(n)`是斐波那契数列的第 n 个数字，`φ` ( `phi`)是黄金分割比例，大约等于`1.61803398875.`

下面是一个 JavaScript 函数，它实现了计算第 n 个斐波那契数的比奈公式:

```
const fibonacci = (n) => {
  const phi = (1 + Math.sqrt(5)) / 2;
  return Math.round(
    (Math.pow(phi, n + 1) - Math.pow(1 - phi, n + 1)) / Math.sqrt(5)
  );
};
```

或者，如果您愿意，您可以使用以下功能:

```
const fibonacci = (n) => {
  const x = n - 1;
  const sqr = 5 ** 0.5;
  const a = (1 + sqr) ** x;
  const b = (1 - sqr) ** x;
  const c = 2 ** x * sqr;
  return Math.round((a - b) / c);
};
```

这个函数有一个参数`n`，它是要计算的斐波那契数列的索引。它返回计算出的斐波那契数。

例如，要计算第 8 个斐波那契数，可以像这样调用函数:

```
console.log(fibonacci(8)); // Output: 13
```

从比奈公式出发，我可以推导出一个公式来检验一个数是否属于斐波纳契数列:

> 如果(5 * N + 4)或(5 * N — 4)是一个完美的平方，那么这个数就是斐波纳契数列的一部分

基于这个定义，我可以编写函数`isFibonacci(n)`:

```
const isFibonacci = (n) => {
  const x1 = 5 * n ** 2 + 4;
  const x2 = 5 * n ** 2 - 4;
  return Number.isInteger(Math.sqrt(x1)) || Number.isInteger(Math.sqrt(x2));
};
```

这个函数有一个参数`n`，它是要检查的数字。如果数字是斐波纳契数，它返回`true`，否则返回`false`。

例如，要检查数字 13 是否是斐波纳契数，您可以像这样调用函数:

```
console.log(isFibonacci(13)); // Output: true
```

我可以更简洁地编写相同的函数:

```
const isFibonacci = (n) =>
  Number.isInteger((5 * n ** 2 + 4) ** 0.5) ||
  Number.isInteger((5 * n ** 2 - 4) ** 0.5);
```

# 如何求一个数在斐波那契数列中的位置？

![](img/e98e20daac57227a3289f4ce56d8e61e.png)

总而言之，我们编写了一个 JavaScript 函数来计算第 n 个斐波那契数列(`fibonacci(n)`)和另一个函数来检查一个数是否属于斐波那契数列(`isFibonacci(n)`)。现在我们只需要写一个函数来计算一个斐波那契数在序列中的位置。

最简单的解决方案也是最耗费资源和时间的:

```
const fibonacciPosition = (n) => { {
  let position = 0;
  let current = 0;
  let next = 1;
  while (current < n) {
    position++;
    let temp = current;
    current = next;
    next = temp + current;
  }
  if (current === n) {
    return position + 1;
  } else {
    return -1;
  }
}
```

我们可以再次用比奈公式写出一个更好的函数:

```
const fibonacciPosition = (n) => {
  // Calculate the golden ratio
  const phi = (1 + Math.sqrt(5)) / 2;

  // Calculate the position using the formula
  const position = Math.log(n * 5 ** 0.5 + 0.5) / Math.log(phi);

  // Return the position as an integer
  return Math.floor(position) + 1;
};
```

但是，有一个问题。数列中的第一个数字很特殊:它们是斐波那契数列本身定义的一部分。尽管这是一种糟糕的编程实践，但在这种情况下，在开始时添加几个条件是值得的:

```
const fibonacciPosition = (n) => {
  if (n === 0) return 1;
  if (n === 1) return 2;

  const phi = (1 + Math.sqrt(5)) / 2;
  const position = Math.log(n * 5 ** 0.5 + 0.5) / Math.log(phi);
  return Math.floor(position) + 1;
};
```

最后，还有一个条件要查，最好是先查。如果这个数字不是斐波那契数，那么我们可以跳过所有的计算并返回值`-1`:

```
const fibonacciPosition = (n) => {
  if (!isFibonacci(n)) return -1;
  if (n === 0) return 1;
  if (n === 1) return 2;

  const phi = (1 + Math.sqrt(5)) / 2;
  const position = Math.log(n * 5 ** 0.5 + 0.5) / Math.log(phi);
  return Math.floor(position) + 1;
};
```

到此，我想我们已经完成了主题。

但是在我们说再见之前，有一个小注意。在函数中，我将数字`1`添加到位置(在`fibonacciPosition(n)`和`fibonacci(n)`中)，使第一个位置有索引`1`。然而，如果我们打算使用数组，因此使用第一个位置的索引为`0`的对象，那么不添加任何东西会更简单。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮件列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

【https://blog.stranianelli.com】原载于 2022 年 12 月 21 日[](https://blog.stranianelli.com/devadvent-2022-21-how-to-check-if-a-given-number-is-fibonacci-number/)**。**

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。******

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***