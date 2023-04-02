# 如何删除 JavaScript 字符串中的前导逗号

> 原文：<https://javascript.plainenglish.io/how-to-remove-a-leading-comma-from-a-javascript-string-e703db36d975?source=collection_archive---------12----------------------->

## 关于如何从 JavaScript 字符串中删除前导逗号的教程。

![](img/cd48b2423ef8aa00271741556a5c1f8f.png)

Photo by [Ryan Antooa](https://unsplash.com/@ryanantooa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望删除 JavaScript 字符串中的前导逗号。

在本文中，我们将研究如何从 JavaScript 字符串中删除前导逗号。

# 使用 String.prototype.substring 方法

我们可以使用 JavaScript string `substring`方法来获取字符串的一部分。

因此，我们可以用它来返回一个没有前导逗号的字符串。

例如，我们可以写:

```
const myOriginalString = ",'first string','more','even more'";
const newString = myOriginalString.substring(1);
console.log(newString)
```

我们用 1 调用`substring`来返回一个字符串从索引 1 到结尾的`myOriginalString`部分。

因此，`newString`就是`"’first string’,’more’,’even more’”`。

# 使用 String.prototype.split 方法

我们可以使用 JavaScript string `split`方法通过分隔符字符串来拆分一个字符串。

例如，我们可以写:

```
const myOriginalString = ",'first string','more','even more'";
const [_, ...rest] = myOriginalString.split(',');
const newString = rest.join(',')
console.log(newString)
```

我们用`','`调用`split`来用逗号分割`myOriginalString`。

然后我们使用 rest 操作符得到一个除了第一个逗号以外的字符串数组。

然后我们用`','`调用`join`，用逗号连接`rest`中的字符串。

因此`newString`具有与之前相同的值。

# 使用 String.prototype.replace 方法

另一种从字符串中删除前导逗号的方法是使用 JavaScript 字符串的`replace`方法。

例如，我们可以写:

```
const myOriginalString = ",'first string','more','even more'";
const newString = myOriginalString.replace(/^,/, '');
console.log(newString)
```

我们用`/^,/`调用`replace`，用空字符串替换前导逗号。

因此`newString`与之前相同。

# 结论

我们可以使用各种字符串方法来去掉字符串中的前导逗号。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*