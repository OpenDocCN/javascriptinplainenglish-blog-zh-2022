# 在 JavaScript 中替换字符串中特定索引处的字符

> 原文：<https://javascript.plainenglish.io/replace-a-character-at-a-particular-index-in-javascript-feac628e2dfc?source=collection_archive---------7----------------------->

![](img/57f3c46e4d15384ea785051d924e6f7b.png)

Photo by [Alvin Engler](https://unsplash.com/@englr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，有几种方法可以替换字符串中特定索引处的字符。

1.  一种方法是将字符串转换为数组，并使用`splice`方法替换数组中的一项，然后将数组转换回字符串。

```
let str = "Hello World";

// Replace the character at index 4 with ','
str = str.split(''); // Convert the string to an array of characters
str.splice(4, 1, ','); // Replace the character at index 4 with ','
str = str.join(''); // Convert the array of characters back to a string
console.log(str); // Output: "Hell, World"
```

2.替换字符串中特定索引处的字符的另一种方法是在特定索引处将字符串分成两个子字符串，然后将子字符串与新字符连接起来。

```
let str = "Hello World";

// Replace the character at index 4 with ','
str = str.substring(0, 4) + ',' + str.substring(5);
console.log(str); // Output: "Hell, World"
```

这些只是 JavaScript 中如何替换字符串中特定索引处的字符的几个例子。您可以选择最适合您需要的方法，并使用它来操作代码中的字符串。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*

****想扩大你的软件创业规模*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。**