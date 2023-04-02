# JavaScript 和 TypeScript 中的 4 个简单问题

> 原文：<https://javascript.plainenglish.io/4-simple-problems-in-javascript-and-typescript-bd1cf508b8fa?source=collection_archive---------11----------------------->

## 毁灭 2022

## 训练 JavaScript 的 4 个简单问题

![](img/0a02d30f9476ad8683b69ef80ab7ee10.png)

今天的倒霉事很简单。为此，我决定解决多个问题。它们都是简单的问题，但对实践很有用。

# 测试 1–2–3

链接到[形](https://www.codewars.com/kata/54bf85e3d5b56c7a05000cf9)

您的团队正在编写一个新奇的文本编辑器，而您的任务是实现行号。

写一个函数，它接受一个字符串列表，并返回每一行前面加上正确的数字。

编号从 1 开始。格式是 n: string。注意冒号和中间的空格。

示例:(输入→输出)

```
[] --> []
["a", "b", "c"] --> ["1: a", "2: b", "3: c"]
```

你可以用一行简单的代码来解决这个问题。我可以将 [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) 方法与模板文字一起使用。

在打字稿中:

```
export const number = (arr: string[]): string[] =>
  arr.map((s, i) => `${++i}: ${s}`);
```

在 JavaScript 中:

```
export const number = (arr) => arr.map((s, i) => `${++i}: ${s}`);
```

# 偶数还是奇数

链接到[形](https://www.codewars.com/kata/53da3dbb4a5168369a0000fe)

![](img/bad350b106d41a9407e266e57c7bd52f.png)

创建一个以整数作为参数的函数，对于偶数返回“Even ”,对于奇数返回“Odd”。

最常见的解决方案是使用[余数运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder) ( `%`)。如果我把一个数除以二，余数等于零，那么这个数就是偶数。

在打字稿中:

```
export const even_or_odd = (n: number): string =>
  n % 2 === 0 ? "Even" : "Odd";
```

在 JavaScript 中:

```
export const even_or_odd = (n) => (n % 2 === 0 ? "Even" : "Odd");
```

但是有一种稍微不同的、数学上更有趣的方法。我们也可以用二进制来表示一个数。我们可以使用[逐位 AND ( &)运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_AND)来检查最后一位的值。为什么只有最后一位的值？因为如果是最后一位是`1`那么这个数字就是奇数，如果是`0`那么就是偶数(如果你好奇的话请看[这个 pdf](http://homepages.math.uic.edu/~scole3/mcs260_fall2011/binary.pdf) )。

在打字稿中:

```
export const even_or_odd = (n: number): string => (n & 1 ? "Odd" : "Even");
```

在 JavaScript 中:

```
export const even_or_odd = (n) => (n & 1 ? "Odd" : "Even");
```

# 返回负数

链接到[形](https://www.codewars.com/kata/55685cd7ad70877c23000102)

![](img/4991332cbd5b4acf088f5e362b78c3ee.png)

在这个简单的作业中，给你一个数字，你必须把它变成负数。但也许数字已经是负数了？

数字可能已经是负数，在这种情况下不需要改变。零(0)不检查任何特定的符号。负零没有数学意义。

例子

```
makeNegative(1);  // return -1
makeNegative(-5); // return -5
makeNegative(0);  // return 0
```

在这种情况下，我知道要得到的数字总是负数。我可以检查它是否已经存在，并且什么也不做。或者我可以取这个数的绝对值，然后返回它的负值。

在打字稿中:

```
export const makeNegative = (num: number): number => -Math.abs(num);
```

在 JavaScript 中:

```
export const makeNegative = (num) => -Math.abs(num);
```

# 将布尔值转换为字符串“是”或“否”。

链接到[形](https://www.codewars.com/kata/53369039d7ab3ac506000467)

完成采用布尔值的方法，并为 true 返回“Yes”字符串，为 false 返回“No”字符串。

在这种情况下，我使用一个[三元运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)来返回正确的值。

在打字稿中:

```
export const boolToWord = (bool: boolean): string => (bool ? "Yes" : "No");
```

在 JavaScript 中:

```
export const boolToWord = (bool) => (bool ? "Yes" : "No");
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，*[*不和*](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*