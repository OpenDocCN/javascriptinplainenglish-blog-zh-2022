# 什么是 JavaScript 模板文字？

> 原文：<https://javascript.plainenglish.io/what-are-javascript-template-literals-cddebc5aa7a4?source=collection_archive---------15----------------------->

![](img/917e9a2c5696d5ab7a2c78626255d91c.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/)

在 ES6 之前，你必须使用**单引号**(')或**双引号**(")来包装字符串，这几乎是你对字符串所能做的一切。

ES6 增加了创建“**模板文字**的可能性，方法是在**反斜线**之间包装字符串，如下所示:

```
const myString = **`**My template literal**`**;
```

您可以在模板文本中使用单引号和双引号:

```
const quote = `Say **"**hello**"** to my little friend!`;
```

您可以创建**多行**字符串，如下所示:

```
const multilineString =
`Once upon a time, 
long,
long ago a king and queen ruled
over a distant land.`;
```

**字符串插值**允许你将变量放入字符串中。

```
const count = 3;
const appleCount = `I have ${count} apples`;
console.log(appleCount) // "I have 3 apples"
```

你也可以把一个完整的表达式放在你的字符串里，就像这样:

```
const amount = 3;
const total = `Total: ${(amount * 5).toFixed(2)}`;
console.log(total) // "Total: 15.00"
```

最初发布在我的[博客](https://blog.ludivineachouri.com/)上。查看我的 [Instagram](https://www.instagram.com/la.dev/) 账号，了解更多关于网络开发的知识。

*更多内容请看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*