# JavaScript 中检查字符串是否包含子串的 10 种方法

> 原文：<https://javascript.plainenglish.io/10-ways-to-check-if-a-string-contains-substring-in-javascript-91639d81b7?source=collection_archive---------10----------------------->

![](img/0ea95e39bc09f5bee599c104bda52659.png)

Image by [Samuele](https://medium.com/@el3um4s)

编程最有趣的事情之一是找到所有可用的方法来解决问题。今天我想找 10 个方法来检查 JavaScript 中一个字符串是否包含子串。

# String.prototype.includes()

让我们从最佳解决方案开始，即`[String.prototype.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)`方法。此方法允许您检查字符串是否包含子字符串，并返回一个布尔值。

```
const string = "Hello World!";

console.log(string.includes("Hello")); // true
console.log(string.includes("!")); // true
console.log(string.includes("Hello World!")); // true

console.log(string.includes("Hello World!!")); // false
```

它的主要限制是区分大小写，所以它不能处理包含大写和小写字符的字符串。

```
const string = "Hello World!";

console.log(string.includes("hello")); // false
```

我们可以通过在执行检查之前将字符串变成小写来解决这个问题。

```
const string = "Hello World!";
const substring = "HeLLo";

console.log(string.toLowerCase().includes(substring.toLowerCase())); // true
```

# String.prototype.indexOf()

第二种方法使用`[String.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)`。此方法返回子字符串在字符串中第一个匹配项的索引，如果没有找到，则返回-1。然后，我可以将索引转换为布尔值。

```
const string = "Hello World!";

console.log(string.indexOf("Hello") !== -1); // true
console.log(!string.indexOf("Hello")); // true
```

同样，该方法区分大小写。

```
const string = "Hello World!";
const substring = "HeLLo";

console.log(!string.indexOf(substring)); // false

console.log(!string.toLowerCase().indexOf(substring.toLowerCase())); // true
```

# 聚合填料

如果我必须使用一个遗留浏览器(我有时会这样做)，仍然可以创建一个 polyfill 来添加`String.prototype.includes()`方法。为此，我再次使用了`String.prototype.indexOf()`,但是用`includes()`方法隐藏了它。

```
if (!String.prototype.includes) {
  String.prototype.includes = function (search, start) {
    "use strict";
    if (typeof start !== "number") {
      start = 0;
    }

    if (start + search.length > this.length) {
      return false;
    } else {
      return this.indexOf(search, start) !== -1;
    }
  };
}
```

# knuth–Morris–Pratt 算法

另一个解决方案是使用[Knuth–Morris–Pratt](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)。该算法始于 20 世纪 70 年代，允许非常快速的搜索，并且经常被用作其他字符串搜索算法的基础。这是 Nayuki 的版本

```
function kmpSearch(pattern, text) {
  if (pattern.length == 0) return 0; // Immediate match

  // Compute longest suffix-prefix table
  var lsp = [0]; // Base case
  for (var i = 1; i < pattern.length; i++) {
    var j = lsp[i - 1]; // Start by assuming we're extending the previous LSP
    while (j > 0 && pattern[i] !== pattern[j]) j = lsp[j - 1];
    if (pattern[i] === pattern[j]) j++;
    lsp.push(j);
  }

  // Walk through text string
  var j = 0; // Number of chars matched in pattern
  for (var i = 0; i < text.length; i++) {
    while (j > 0 && text[i] != pattern[j]) j = lsp[j - 1]; // Fall back in the pattern
    if (text[i] == pattern[j]) {
      j++; // Next char matched, increment position
      if (j == pattern.length) return i - (j - 1);
    }
  }
  return -1; // Not found
}

console.log(kmpSearch("ays", "haystack") != -1); // true
console.log(kmpSearch("asdf", "haystack") != -1); // false
```

# 其他解决方案

![](img/dd33e17af4f771408633f76f57da1e10.png)

Image by [Samuele](https://medium.com/@el3um4s)

但这不是我们唯一可以走的路。还有其他的可能性，只要你稍微推动一下 JavaScript。我不推荐使用它们，但是它们对于理解 JavaScript 如何工作很有意思。

在接下来的例子中，我将使用两个变量，`string`和`substring`，它们将分别包含要搜索的字符串和子字符串。

```
const string = "Hello World!";
const substring = "Hello";
```

我可以使用`[String.prototype.match()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)`来匹配正则表达式搜索的结果。如果搜索一无所获，则返回`null`。然后，我将结果转换成一个布尔值。

```
console.log(!!string.match(substring)); // true
```

类似地，如果搜索一无所获,`[String.prototype.search()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search)`将返回`-1`。所以我只检查结果是否大于等于零。

```
console.log(string.search(substring) >= 0); // true
```

另一种方法是用空值替换子字符串，并检查字符串的长度是否发生了变化。或者我也可以简单地验证它不等于它本身。为此，我使用了`[String.prototype.replace()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)`方法

```
console.log(string.replace(substring, "") != string); // true
console.log(string.replace(substring, "").length != string.length); // true
```

# startWith()和 endsWith()

最后，如果我只想检查开始或结束，我可以使用`[String.prototype.startsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith)`和`[String.prototype.endsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith)`

```
const string = "Hello World!";

console.log(string.startsWith("Hello")); // true
console.log(string.endsWith("!")); // true
```

这两种方法在特定的情况下会很有用，而且可能会比你想象的更多。但如果你想做一个通用的搜索，最好使用另一种解决方案。

# 结论

好吧，我要说这十个解决方案就够了。除了与这个具体案例相关的娱乐之外，花点时间探索各种可用的解决方案总是值得的。第一个想法并不总是最好的。而且，总的来说，这是一个更好地了解一个话题和提高技能的方法。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****