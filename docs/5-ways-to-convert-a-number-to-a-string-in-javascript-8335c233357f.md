# 在 JavaScript 中将数字转换成字符串的 5 种方法

> 原文：<https://javascript.plainenglish.io/5-ways-to-convert-a-number-to-a-string-in-javascript-8335c233357f?source=collection_archive---------16----------------------->

## 毁灭 2022

## 或者，有时最简单的事情会揭示意想不到的解决方案

![](img/939ada4a0e69a7a06d6213b2d46d8165.png)

Image by [Samuele](https://medium.com/@el3um4s)

今天这个 DevAdvent 2022 的问题真的很简单。我可以把它归为 JavaScript 中的基本知识:如何将数字转换成字符串。但是虽然是个简单的问题，却有各种各样的解决方法。让我们看看它们是什么。

# 问题是

链接到[形](https://www.codewars.com/kata/5265326f5fda8eb1160004c8)

我们需要一个能将数字(整数)转换成字符串的函数。你知道实现这一目标的方法吗？

例子

```
123  --> "123"
999  --> "999"
-100 --> "-100"
```

# 我的解决方案:模板文字

![](img/b4f1a5f6c88ac39558130ccfbd76c700.png)

Image by [Samuele](https://medium.com/@el3um4s)

我想到的第一个解决方案是使用[模板文字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)。Mozilla 是这样定义它们的:

> 模板文字是由反斜杠(`)字符分隔的文字，允许多行字符串、带有嵌入式表达式的字符串插值以及称为标记模板的特殊构造。

因此，这是我的解决方案:

```
const numberToString = (x) => `${x}`;
```

# Number.toString()

![](img/e2f5e4740c5427713df75dc44876a855.png)

Image by [Samuele](https://medium.com/@el3um4s)

但这不是唯一的出路。一种解决方案是使用 [Number.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString) 方法。在某些情况下，这甚至是最好的解决方案。

```
const numberToString = (x) => x.toString();
```

这个方法有一个名为`radix`的参数。基数是在范围`2`到`36`内的整数，指定用于表示数值的基数。默认为 10。

基本上，它允许你将一个数从一个基数转换到另一个基数，并得到一个字符串。唯一要记住的是，要在一个数字上(而不是在一个变量上)直接使用它，你需要用音调括号把数字本身括起来。

```
10.toString(); // SyntaxError: Invalid or unexpected token
(10).toString(); // "10"
(10).toString(2); // "1010"
(10).toString(8); // "12"
(10).toString(16); // "a"
```

# 字符串()

在 JavaScript 中将数字转换成字符串的另一种方法是使用 [String()构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/String)。String 构造函数用于创建一个新的 String 对象。当作为函数调用时，它执行到原始字符串的类型转换。

```
const numberToString = (x) => x.toString();
```

但是如果我们决定走这条路，我们可以进一步简化代码:

```
const numberToString = String;
```

为此，我将 numberToString 常量与 String()构造函数结合起来。所以写`numberToString(10)`和写`String(10)`是一样的。这是口味的问题。

# 串并置

另一种可能的变化是使用字符串连接。这迫使 JS 自动将数字转换成字符串。这是我的解决方案的变体:

```
const numberToString = (x) => "" + x;
```

# 自定义 toString()

![](img/3b6d20f7c2943b795c0d16b7bc5f2c67.png)

Image by [Samuele](https://medium.com/@el3um4s)

最后一个解决方案是最复杂的。但肯定是最有趣的。它是关于重现 toString()方法，来分析它的算法。这段代码旨在做`toString()`所做的事情(针对整数)，但不使用内置函数。

不是我的代码，而是[xor mias’](https://www.codewars.com/users/XoRMiAS)。

```
function numberToString(num) {
  //create a new empty string in which the result will be written
  var str = "";

  //Check, whether the number is positive or negative. The multiplier 1 or -1 will be saved for later
  const mult = num < 0 ? -1 : 1;

  //Take the absolut value of num. Could also be done with Math.abs
  num *= mult;

  //Loop, which will run as often as num has digits
  do {
    //Take the least significant digit of num (num % 10), add 48 and get the associated ascii character. The number 0 has the ascii value of 48, 1 = 49... 9 = 57.
    //Then prepend that character to the string.
    str = String.fromCharCode((num % 10) + 48) + str;

    //Remove the least significant digit from num. (Divide by ten, then round down)
    num = ~~(num / 10);
  } while (num > 0);

  //If the input number was negative, prepend a -.
  if (mult < 0) str = "-" + str;
  return str;
}
```

我想出了 5 种将数字转换成字符串的方法。从最简单到最复杂。最终，这不是一个微不足道的问题。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容请看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*