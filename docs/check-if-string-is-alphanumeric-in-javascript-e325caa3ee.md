# 检查 JavaScript 中的字符串是否为字母数字

> 原文：<https://javascript.plainenglish.io/check-if-string-is-alphanumeric-in-javascript-e325caa3ee?source=collection_archive---------1----------------------->

![](img/595bc07b412964757f51566e852994dd.png)

Photo by [Federico Respini](https://unsplash.com/@federicorespini?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，经常需要检查字符串是否是字母数字的，这意味着它只包含字母和数字，不包含其他字符。这对于验证非常有用，例如检查用户的密码是否满足某些要求。在本文中，我们将探索 JavaScript 中检查字符串是否为字母数字的不同方法。

1.  以下是如何使用正则表达式检查字符串是否为字母数字的示例:

```
function isAlphanumeric(str) {
  return /^[a-zA-Z0-9]+$/.test(str);
}

console.log(isAlphanumeric("abc123"));  // true
console.log(isAlphanumeric("abc!@#"));  // false
console.log(isAlphanumeric("123456"));  // true
console.log(isAlphanumeric(""));  // false
```

正则表达式`/^[a-zA-Z0-9]+$/`测试字符串是否只包含字母和数字。`^`和`$`符号将模式锚定在字符串的开头和结尾，这样正则表达式将只匹配整个字符串，而不仅仅是一部分。字符集后的`+`符号表示模式应该匹配一个或多个字符。

2.你也可以使用`String.prototype.match()`方法来检查一个字符串是否是字母数字的。该方法返回一个匹配数组，如果字符串与模式不匹配，则返回`null`。下面是一个如何使用`String.prototype.match()`的例子:

```
function isAlphanumeric(str) {
  return str.match(/^[a-zA-Z0-9]+$/) !== null;
}

console.log(isAlphanumeric("abc123"));  // true
console.log(isAlphanumeric("abc!@#"));  // false
console.log(isAlphanumeric("123456"));  // true
console.log(isAlphanumeric(""));  // false
```

3.您也可以使用`String.prototype.search()`方法来检查一个字符串是否是字母数字的。

```
function isAlphanumeric(str) {
  return str.search(/^[a-zA-Z0-9]+$/) !== -1;
}

console.log(isAlphanumeric("abc123"));  // true
console.log(isAlphanumeric("abc!@#"));  // false
console.log(isAlphanumeric("123456"));  // true
console.log(isAlphanumeric(""));  // false
```

该方法返回第一个匹配项的索引，如果字符串与模式不匹配，则返回`-1`。下面是一个如何使用`String.prototype.search()`的例子。

上面提到的所有确定字符串是否是字母数字的方法都很有效，你可以使用其中的任何一种。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*