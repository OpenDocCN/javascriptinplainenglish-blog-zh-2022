# 如何在 Javascript 中获取查询字符串？

> 原文：<https://javascript.plainenglish.io/how-to-get-query-string-in-javascript-596edf1ffb34?source=collection_archive---------21----------------------->

![](img/ce65ecabe95395097cb0169b90f4e08b.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要在 JavaScript 中获取查询字符串值，可以使用`URLSearchParams`对象，它提供了一种访问查询字符串参数值的简单方法。这里有一个如何使用它的例子:

```
// Get the current URL
const currentUrl = new URL(window.location.href);
// Get the value of the "name" query string parameter
const name = currentUrl.searchParams.get("name");
console.log(name); // Outputs the value of the "name" query string parameter
```

您还可以使用`URLSearchParams`对象来设置查询字符串值并更新 URL:

```
// Set the value of the "name" query string parameter to "John"
currentUrl.searchParams.set("name", "John");
console.log(currentUrl.href); // Outputs the updated URL with the "name" query string parameter set to "John"
```

您还可以使用`URLSearchParams`对象迭代所有查询字符串参数:

```
const searchParams = new URLSearchParams(currentUrl.search);
for (const [key, value] of searchParams) {
  console.log(`${key}: ${value}`);
}
```

总之，`URLSearchParams`对象是一种在 JavaScript 中访问和操作查询字符串值的便捷方式。它为获取、设置和迭代查询字符串参数提供了一个简单的接口。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及*******不和****

****想扩大你的软件创业规模*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。**