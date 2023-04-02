# 每个 Web 开发人员都应该知道的 6 个有用的 CSS 函数

> 原文：<https://javascript.plainenglish.io/6-useful-css-functions-every-web-developer-should-know-4be9ad59183f?source=collection_archive---------5----------------------->

## 可以在 CSS 代码中使用的强大功能。

![](img/681c69dcc4fec1c5e50a95d7e3f9d94d.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 是每个 web 开发人员的必备样式表语言。它让我们可以设计网页的样式，并使它们具有响应性。此外，借助 flexbox 和 grid 等新的 CSS 特性，我们可以轻松地为网页创建复杂的布局。

有了 CSS，天空才是极限。你只需要有点创造力，并且很好地掌握这门语言。

像所有其他不同的语言一样，CSS 也有自己的函数可以使用。这些函数可以放在你放置属性值的地方。在某些情况下，它们可以伴随另一个值声明。一些 CSS 函数甚至可以嵌套到其他函数中，让你一次完成很多事情。

在这篇文章中，我将与你分享一些有用的 CSS 函数，这些函数是你作为一个 web 开发人员应该知道的。所以让我们开始吧。

# 1.函数 calc

我们可以使用 CSS 中的函数`calc()`轻松地进行计算(`+`、`-`、`*`、`/`)，以确定属性值。

该函数将计算作为其参数。那么让我们来看一个简单的例子:

```
div{
 width: **calc(100vw - 50px);**
}
```

正如你在上面看到的，我们使用了函数`calc()`来计算我们想要的精确宽度，而不需要改变单位。所以这是一个完美的函数，可以在你的 CSS 代码中自动完成这些计算。

# 2.函数 var

如果你使用普通的 CSS，这个函数非常有用。它允许你给一个属性一个 CSS 变量的值。所以这个函数`var()`对于创建 CSS 变量并在代码的不同地方使用它们是很有用的。

下面是一个代码示例:

```
:root {
  --main-bg-color: coral;
  --main-padding: 15px;
}/* using the var function to insert variables as property values */
div{
  background-color: **var(--main-bg-color);**
  padding: **var(--main-padding);**
}
```

结果，由于 var 函数，div 将有一个背景色`coral`和 15px 的填充。

# 3.URL 函数

函数`url()`用于描述或识别我们项目中一个文件的位置。该功能经常与属性一起使用，如:`background-image`、`list-style`、`content`、`border`等。

下面是一个代码示例:

```
.element{
 background-image: **url("pic.gif");**
 list-style-image: **url('../images/pic.jpg');**
 content: **url("pdficon.jpg");**
 cursor: **url(mycursor.cur);**
}
```

如您所见，该函数允许我们将文件或媒体资源设置为 CSS 中某些属性的值。

# 4.rgb()和 rgba()函数

函数`rgb()`和`rgba()`用于描述 CSS 中的颜色级别。

这里有一个例子:

```
#div1{
 color: **rgb(0, 0, 6)**;
}#div2{
 color: **rgba(0, 0, 0, 1)**;
}
```

# 5.函数的作用是

函数`hsl()`代表色调、饱和度和亮度。它允许我们使用这些参数来定义颜色的级别。

下面是一个代码示例:

```
div{
 background: **hsl(0, 100%, 50%)**;
}
```

# 6.函数:not()

CSS 中的函数`:not()`用于将样式应用于没有特定类或 ID 的特定元素。

例如，我们可以使用函数`:not()`将样式仅应用于一个没有名为`.pic`的类的图像。

下面是一个例子:

```
img**:not(.pic)**{
    padding: 0;
    opacity: .5;
}
```

# 结论

正如您在上面看到的，这是您可以在代码中使用的有用 CSS 函数的一个小列表。还有很多其他函数我们没有涉及，因为这个列表会很长，但是我可能会在以后的文章中涉及一个很大的列表。

*感谢您阅读这篇文章。此外，如果你发现我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [***这里***](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得无限制的访问媒体上的所有文章，并支持我们作为作家。*

**更多阅读:**

[](/10-powerful-javascript-code-snippets-that-you-should-know-217363914589) [## 你应该知道的 10 个强大的 JavaScript 代码片段

### 每个 web 开发人员都应该知道的 JavaScript 代码片段。

javascript.plainenglish.io](/10-powerful-javascript-code-snippets-that-you-should-know-217363914589) 

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*