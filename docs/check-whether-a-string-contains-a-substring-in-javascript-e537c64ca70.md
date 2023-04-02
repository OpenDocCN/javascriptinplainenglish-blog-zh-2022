# 在 JavaScript 中检查字符串是否包含子字符串

> 原文：<https://javascript.plainenglish.io/check-whether-a-string-contains-a-substring-in-javascript-e537c64ca70?source=collection_archive---------17----------------------->

![](img/35ec50e5e890e6828c22645cb7bc3a2e.png)

Photo by [Gabriella Clare Marino](https://unsplash.com/@gabiontheroad?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要在 JavaScript 中检查一个字符串是否包含子串，我们可以使用内置的方法。在字符串中包含()。

示例:

```
let str = "Hello World!";
if (str.includes("Hello")) {
    console.log("The string contains the substring 'Hello'");
} else {
    console.log("The string does not contain the substring 'Hello'");
}
```

**输出:**“字符串包含子字符串‘Hello’”

我们还可以使用 indexOf()方法来检查一个字符串是否包含子串。如果 indexOf()方法返回大于或等于 0 的值，则意味着该子串存在于字符串中。

**举例:**

```
let str = "Hello World!";
if (str.indexOf("Hello") >= 0) {
    console.log("The string contains the substring 'Hello'");
} else {
    console.log("The string does not contain the substring 'Hello'");
}
```

**输出:**“字符串包含子字符串‘Hello’”

## **结论**

总之，双方。在 JavaScript 中，可以使用 includes()和 indexOf()方法来检查字符串是否包含子字符串。的。includes()方法是一种较新的方法，在某些情况下可能更容易使用，但 indexOf()方法是一种使用更广泛的方法，可能更为一些开发人员所熟悉。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*