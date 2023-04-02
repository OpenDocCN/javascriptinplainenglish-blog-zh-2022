# 如何在 JavaScript 和 TypeScript 中反转字符串

> 原文：<https://javascript.plainenglish.io/how-to-reverse-a-string-in-javascript-and-typescript-e9bc700eb28b?source=collection_archive---------3----------------------->

## 毁灭 2022

## 或者说，如何一起使用 Array.map()和 Array.reverse()来修改一个句子

![](img/b3e332f7097918408f46578242560167.png)

Image by [Samuele](https://medium.com/@el3um4s)

今天的问题是如何颠倒一个单词中字母的顺序，以及一个句子中每个单词的顺序。这是一个相当简单的问题，但不应该被低估。它允许你测试你的数组和字符串知识。

# 问题是

链接到[形](https://www.codewars.com/kata/5259b20d6021e9e14c0010d4)

![](img/7073dfc50d33875875850473bf5d2137.png)

Image by [Samuele](https://medium.com/@el3um4s)

完成接受字符串参数的函数，并反转字符串中的每个单词。应该保留字符串中的所有空格。

例子

```
"This is an example!" ==> "sihT si na !elpmaxe"
"double  spaces"      ==> "elbuod  secaps"
```

# 解决方案

![](img/421371d51151e80489938e7472371ee2.png)

Image by [Samuele](https://medium.com/@el3um4s)

首先要做的是把问题读好。这不仅仅是颠倒单词或短语中字母的顺序。这不仅仅是颠倒单词或短语中字母的顺序。但是从这部分开始，去理解如何处理问题，可能是有用的。

所以，我需要一个函数将字符串转换成字母数组。我可以使用[扩展操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)来完成这项工作。

```
const reverseString = (str: string): string[] => [...str];
```

在得到一个数组后，我使用了 [Array.reverse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) 方法来…反转数组元素的顺序。

```
const reverseString = (str: string): string[] => [...str].reverse();
```

最后，我再次连接各个元素以获得一个字符串(我使用了 [Array.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 方法)

```
const reverseString = (str: string): string => [...str].reverse().join("");
```

现在我有了一个可以重用的函数来颠倒单词中字母的顺序。我只需要把它应用到一个句子中。但是首先我必须把每个句子分解成单词。我可以使用 [String.split()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法做到这一点。

```
const words: string[] = str.split(" ");
```

为了改变每个单词，我使用了结合 reverseString()函数的 [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 方法。这样我就得到了这个函数:

```
const reverseString = (str: string): string => [...str].reverse().join("");

export function reverseWords(str: string): string {
  const words: string[] = str.split(" ");
  const invertedWords: string[] = words.map((w) => reverseString(w));
  const result: string = invertedWords.join(" ");
  return result;
}
```

我可以这样折射这个函数:

```
const reverseString = (str: string): string => [...str].reverse().join("");

export function reverseWords(str: string): string {
  const invertedWords: string = str
    .split(" ")
    .map((w) => reverseString(w))
    .join(" ");
  return invertedWords;
}
```

然后像这样:

```
const reverseString = (str: string): string => [...str].reverse().join("");

export const reverseWords = (s: string): string =>
  s
    .split(" ")
    .map((w) => reverseString(w))
    .join(" ");
```

JavaScript 版本呢？我去掉这些类型，得到了:

```
const reverseString = (str) => [...str].reverse().join("");

export const reverseWords = (s) =>
  s
    .split(" ")
    .map((w) => reverseString(w))
    .join(" ");
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***