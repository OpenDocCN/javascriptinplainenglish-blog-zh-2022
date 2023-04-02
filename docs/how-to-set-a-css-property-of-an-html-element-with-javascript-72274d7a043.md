# 如何用 JavaScript 设置一个 HTML 元素的 CSS 属性？

> 原文：<https://javascript.plainenglish.io/how-to-set-a-css-property-of-an-html-element-with-javascript-72274d7a043?source=collection_archive---------7----------------------->

![](img/1a126a51d151c1c63d48b29d31b7f9b6.png)

Photo by [Joyful](https://unsplash.com/@joyfulcaptures?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 设置 HTML 元素的 CSS 属性。

在本文中，我们将看看如何用 JavaScript 设置 HTML 元素的 CSS 属性。

# 通过设置样式属性，用 JavaScript 设置 HTML 元素的 CSS 属性

我们可以用 JavaScript 通过设置`style`属性的一个属性来设置 HTML 元素的 CSS 属性。

例如，我们可以写:

```
const element = document.createElement('div');
element.textContent = 'hello world'
element.style.backgroundColor = "lightgreen";
document.body.append(element)
```

我们用`'div'`调用`document.createElement`来创建一个 div 元素。

然后我们将`textContent`设置为一个字符串，向 div 中添加一些文本。

接下来，我们设置`style.backgroundColor`属性来设置它的背景颜色。

任何包含多个单词的 CSS 属性都是 camel 大小写，而不是 kebab 大小写。

最后，我们调用`document.body.append`将 div 追加到`body`元素中。

# 通过设置 cssText 属性，用 JavaScript 设置 HTML 元素的 CSS 属性

用 JavaScript 设置 HTML 元素样式的另一种方法是将`style.cssText`属性设置为包含一些 CSS 样式的字符串。

例如，我们可以写:

```
const element = document.createElement('div');
element.textContent = 'hello world'
element.style.cssText = 'background-color: lightgreen';
document.body.append(element)
```

我们将`element.style.cssText`设置为带有一些 CSS 样式的字符串。

该字符串只有常规的 CSS 代码来设置样式。

因此，我们得到了与上一个例子相同的结果。

# 结论

我们可以通过在`style`属性或`style.cssText`属性中设置样式属性来设置 CSS 文本，从而设置 HTML 元素的 CSS 样式。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*