# JavaScript 中什么是真和假

> 原文：<https://javascript.plainenglish.io/what-are-truthy-and-falsy-in-javascript-19a4fea80108?source=collection_archive---------16----------------------->

## 理解 JavaScript 中的真理和谬误

![](img/ddd4d66dc9e77c7dc4db171bde9a8a97.png)

在 JavaScript 中，基本类型之一是 boolean。布尔值是一个或真或假的值。此外，JavaScript 中的所有其他值不是 true 就是 falsy。这意味着尽管该值不明确地为真或假，但是该值可以被认为是真或假。

人们更容易回忆起虚假的价值观，因为这样的价值观更少。任何非虚假的价值都是真实的。JavaScript 中的 falsy 值如下:

*   错误的
*   0
*   " "(空字符串)
*   圆盘烤饼
*   空
*   不明确的

当你使用条件句时，理解一个值是真还是假特别有帮助。让我们看一个例子来阐明这一点。

```
let ourValue = "a";if (ourValue) {
  console.log("I am truthy");
} else {
  console.log("I am falsy");
}//Returns ---> I am truthy
```

在上面的例子中，我们声明了一个名为 *ourValue* 的变量，并把字母 *a* 赋给这个变量。接下来，我们创建一个 if/else 语句，该语句将根据条件是否为真来返回控制台日志。我们把我是真的控制台日志打印到屏幕上，因为在屏幕下面，一个不为空的字符串是真的。让我们再看一次同样的例子，但是这次我们将把 *ourValue* 设置为一个假值。

```
let ourValue = NaN;if (ourValue) {
  console.log("I am truthy");
} else {
  console.log("I am falsy");
}//Returns ---> I am falsy
```

这一次我们将 *ourValue* 设置为 *NaN* ，这是一个错误的值。当语句运行时，屏幕上显示出*我是 falsy* 。当我们检查空值时，这种方法特别有用，它节省了我们编写更多代码和使用等式运算符的时间。

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。****