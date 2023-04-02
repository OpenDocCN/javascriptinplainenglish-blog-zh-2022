# 如何用 JavaScript 获取文件扩展名？

> 原文：<https://javascript.plainenglish.io/how-to-get-file-extensions-with-javascript-af4c6536b849?source=collection_archive---------5----------------------->

![](img/dd47283a5cc03d3eec7ced9f49923017.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想从文件路径中获取文件扩展名。

在本文中，我们将研究如何用 JavaScript 从路径中获取文件扩展名。

# 字符串.原型. split

我们可以使用 JavaScript 字符串的`split`方法，通过获取路径中最后一个点之后的子字符串来获取文件路径的扩展名。

例如，我们可以写:

```
const ext = '/home/foo/bar.txt'.split('.').pop();
console.log(ext)
```

我们用点号调用`split`来按点号拆分字符串。

然后我们对它调用`pop`来移除拆分字符串中的最后一项并返回它。

所以`ext`就是`'txt'`。

# 正则表达式匹配

我们还可以用 Regex 匹配文件扩展名。

例如，我们可以写:

```
const filename = '/home/foo/bar.txt'
const ext = (/[.]/.exec(filename)) ? /[^.]+$/.exec(filename) : undefined;
console.log(ext)
```

我们有带文件路径的`filename`。

然后我们在带有`exec`的`filename`字符串中寻找点。

如果字符串中有任何点，那么我们检查任何以字符串末尾的点开始的内容。

美元符号表示在字符串的末尾。

而`^`的意思是开始于。

这将是文件扩展名。

因此，我们得到和以前一样的结果。

# String.prototype.substring 和 String.prototype.lastIndexOf

我们可以使用一个字符串的`lastIndexOf`方法来获取一个子字符串的最后一个实例的索引。

我们可以将它与`substring`方法结合起来提取文件扩展名子串。

例如，我们可以写:

```
const filename = '/home/foo/bar.txt'
const ext = filename.substring(filename.lastIndexOf('.') + 1, filename.length) || filename;
console.log(ext)
```

我们以`filename.lastIndexOf(‘.’) + 1`为起始索引调用`substring`。

而`filename.length`是结束索引。

那么`ext`应该与另一个值相同。

# String.prototype.slice 和 String.prototype.lastIndexOf

我们可以使用`slice`而不是`substring`从 JavaScript 字符串中提取子串。

因此，我们可以用它从一个文件路径中获取文件扩展名。

为了使用它，我们写:

```
const filename = '/home/foo/bar.txt'
const ext = filename.slice((Math.max(0, filename.lastIndexOf(".")) || Infinity) + 1)
console.log(ext)
```

我们找到索引 0 和由`lastIndexOf`返回的索引之间的最大值，以获得该点的最后一个索引。

路径可以以点开始，所以索引可能是 0。

然后我们加 1 得到不包括点本身的索引。

因此，我们得到和以前一样的结果。

# 结论

我们可以使用各种 JavaScript 字符串方法从字符串中提取文件扩展名。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*