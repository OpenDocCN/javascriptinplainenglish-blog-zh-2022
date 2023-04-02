# 如何替换 JavaScript 中出现的所有字符串

> 原文：<https://javascript.plainenglish.io/how-to-replace-all-occurrences-of-a-string-in-javascript-7f45dbb27710?source=collection_archive---------14----------------------->

![](img/3738ff19c108b20acf79b8b36e8a031b.png)

Photo by [Anne Nygård](https://unsplash.com/es/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有几种方法可以替换 JavaScript 中出现的所有字符串:

1.  使用`replace()`方法:

```
let str = "Hello, welcome to the world of JavaScript!";
str = str.replace(/JavaScript/g, "HTML");
console.log(str); // Output: "Hello, welcome to the world of HTML!"
```

在上面的例子中，`replace()`方法用于将所有出现的字符串“JavaScript”替换为字符串“HTML”。`g`标志表示替换应该是全局的，即它应该替换搜索字符串的所有出现。

2.使用`split()`和`join()`方法:

```
let str = "Hello, welcome to the world of JavaScript!";
str = str.split("JavaScript").join("HTML");
console.log(str); // Output: "Hello, welcome to the world of HTML!"
```

在这个例子中，`split()`方法用于将原始字符串分割成一个子字符串数组，使用“JavaScript”作为分隔符。然后使用`join()`方法将数组元素连接成一个字符串，使用“HTML”作为分隔符。这有效地将所有出现的“JavaScript”替换为“HTML”。

3.使用正则表达式和循环:

```
let str = "Hello, welcome to the world of JavaScript!";
let regex = /JavaScript/g;
let newStr = "";
while ((result = regex.exec(str)) !== null) {
    newStr += str.slice(0, result.index) + "HTML";
    str = str.slice(result.index + result[0].length);
}
newStr += str;
console.log(newStr); // Output: "Hello, welcome to the world of HTML!"
```

在本例中，正则表达式用于查找原始字符串中所有出现的“JavaScript”。然后使用一个循环迭代匹配项，匹配的字符串在新字符串中被替换为“HTML”。

## 结论:

`replace()`方法是替换 JavaScript 中所有出现的字符串的最简单易用的选项。但是，如果您需要对替换过程进行更多的控制，或者需要执行更复杂的字符串操作，那么`split()`和`join()`或者正则表达式和循环方法可能更合适。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*