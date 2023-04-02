# 如何用 JavaScript 对字母数字字符串进行排序？

> 原文：<https://javascript.plainenglish.io/how-to-sort-alphanumeric-strings-with-javascript-106a35d38f33?source=collection_archive---------5----------------------->

## 用 JavaScript 对字母数字字符串进行排序的指南。

![](img/51a5f381ab60a51a409ab8d3596d2d0a.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 对字母数字字符串进行排序。

在本文中，我们将看看如何用 JavaScript 对字母数字字符串进行排序。

# String.prototype.localeCompare

我们可以使用 string `localeCompare`方法来比较字符串，以便对它们进行排序。

例如，我们可以写:

```
const arr = [
  '123asd',
  '19asd',
  '12345asd',
  'asd123',
  'asd12',
]
const sorted = arr.sort((a, b) => {
  return a.localeCompare(b, undefined, {
    numeric: true,
    sensitivity: 'base'
  })
})
console.log(sorted)
```

我们称`localeCompare`自然是为了比较`a`和`b`。

我们将`numeric`设置为`true`来比较`a`和`b`的数值部分。

`sensitivity`设置为`'base'`比较大小写和字母。

因此，`sorted`是:

```
["19asd", "123asd", "12345asd", "asd12", "asd123"]
```

# 使用 Intl。校对机

此外，我们可以使用`Intl.Collator`构造函数来创建一个 collator 实例，该实例使用`compare`方法来比较两个字符串。

例如，我们可以写:

```
const arr = [
  '123asd',
  '19asd',
  '12345asd',
  'asd123',
  'asd12',
]
const collator = new Intl.Collator(undefined, {
  numeric: true,
  sensitivity: 'base'
});
const sorted = arr.sort((a, b) => {
  return collator.compare(a, b)
})
console.log(sorted)
```

选项与`localeCompare`相同。

`compare`获取我们想要比较的两个字符串。

然后`sorted`是和之前一样的结果。

# 结论

这就是我们如何用本地 JavaScript 方法自然地对字母数字字符串进行排序。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*