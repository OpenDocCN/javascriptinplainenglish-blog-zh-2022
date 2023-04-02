# 你可能不知道的 6 个很棒的 CSS 速记属性

> 原文：<https://javascript.plainenglish.io/6-awesome-css-shorthand-properties-that-you-probably-dont-know-f593b21ebf3?source=collection_archive---------7----------------------->

## 每个开发人员都应该知道的有用的 CSS 速记属性列表。

![](img/6bdbc57dd45a11fcc8544dd6da5d322d.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 是一种非常棒的 web 样式表语言。它让我们可以让网页看起来更漂亮，让用户赏心悦目。你可以随心所欲地设计任何网页的样式，只需使用 CSS 就可以让它在不同的设备上完全响应。

这种语言有很多有用的特性和属性，可供开发人员使用。但是写好 CSS 是需要时间的。有时，仅仅为了使用 CSS 样式化一个 HTML 元素，你将不得不在你的代码中使用许多属性。结果，你可能会得到一个很大的 CSS 文件，这会影响你的站点的性能或者很难阅读。

这就是为什么优化您的 CSS 代码并使其尽可能短总是一个好的做法。这也可以帮助您更快地编写代码，提高工作效率。幸运的是，有很多方法可以让你的 CSS 文件更小，编写的代码行更少。使用 CSS 快捷键是一个很好的方法。

CSS 速记属性是一个简单的属性，它允许您在其上插入多个 CSS 值，而不必使用多行代码。

在本文中，我将与您分享一些有用的 CSS 速记属性，它们可以帮助您编写更少的代码，并使您的 CSS 文件更小。所以让我们开始吧。

# 1.边框速记

CSS 边框速记属性`border`允许你在一行代码中组合多个边框属性。

因此属性`border`在一行代码中组合了下面的 CSS 属性:

*   `border-width`
*   `border-style`
*   `border-color`

下面是代码示例:

*手写(在使用速记之前):*

```
div{
 border-width: 2px;
 border-style: solid;
 border-color: #000;
}
```

***速记:***

```
div{
 **border: 2px solid #000;**
}
```

如你所见，当使用简写时，我们能够用一行 CSS 代码实现同样的事情。

# 2.字体速记

字体速记`font`将多个 CSS 属性合并成一个属性，允许我们向这个属性插入多个值。

速记属性`font`结合了以下所有属性:

*   `font-style`
*   `font-weight`
*   `font-size`
*   `line-height`
*   `font-family`

下面是代码示例:

手写(在使用速记之前):

```
div{
 font-style: italic;
 font-weight: bold;
 font-size: 1.1rem;
 line-height: 1.2;
 font-family: Arial, sans-serif;
}
```

***速记:***

```
div{
 **font: italic bold 1.1rem/1.2 Arial, sans-serif;**
}
```

# 3.插图速记

CSS 速记属性`inset`将允许你在一行代码中从各个方向定位元素。

它是以下属性的简写:

*   `top`
*   `right`
*   `bottom`
*   `left`

下面是代码示例:

*手写(在使用速记之前):*

```
div{
 top: 3px;
 right: 5px;
 bottom: 6px;
 left: 4px;
}
```

***速记:***

```
div{
  */* top right bottom left */*
 **inset: 3px 5px 6px 4px;**
}
```

如你所见，属性`inset`允许我们在一行 CSS 代码中组合上述 4 个定位属性。这是一个可怕的速记，不是吗？

# 4.填充速记

CSS 简写`padding`允许你在一行代码中从各个方向(顶部、左侧、右侧和底部)向元素添加填充空间。

它允许您将以下所有属性合并为一个属性:

*   `padding-top`
*   `padding-right`
*   `padding-bottom`
*   `padding-left`

下面是代码示例:

*手写(在使用速记之前):*

```
div{
 padding-top: 3px;
 padding-right: 5px;
 padding-bottom: 6px;
 padding-left: 4px;
}
```

***速记:***

```
div{
  */* top right bottom left */*
 **padding: 3px 5px 6px 4px;**
}
```

# 5.空白速记

CSS 简写`margin`允许你在一行代码中从各个方向(上、下、左、右)给元素添加空白。

它允许您将所有低于毛利的属性合并为一个属性:

*   `margin-top`
*   `margin-right`
*   `margin-bottom`
*   `margin-left`

下面是代码示例:

*手写(在使用速记之前):*

```
div{
 margin-top: 3px;
 margin-right: 5px;
 margin-bottom: 6px;
 margin-left: 4px;
}
```

***速记:***

```
div{
  */* top right bottom left */*
 **margin****: 3px 5px 6px 4px;**
}
```

# 6.列表速记

属性`list-style`将允许您使用一行代码插入所有 CSS 列表样式属性的值。

它是下面所有列表样式属性的简写:

*   `list-style-type`
*   `list-style-position`
*   `list-style-image`

下面是代码示例:

*手写(在使用速记之前):*

```
div{
 list-style-type: disc;
 list-style-position: inside;
 list-style-image: url(disc.png);
}
```

***速记:***

```
div{
 **list-style: disc inside url(disc.png);**
}
```

就是这样，属性`list-style`是一个很好的简写，您可以用它在一行代码中编写所有列表样式的属性。

# 结论

正如你在上面看到的，这是一个很棒的 CSS 简写属性列表，开发者可以使用它。如果您想节省一些 CSS 代码行，节省时间，并制作更小的 CSS 文件以提高站点或应用程序的性能，这些快捷方式非常有用。

*感谢您阅读本文。此外，如果你觉得我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [***这里***](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得无限制的访问媒体上的所有文章，并支持我们作为作家。*

[](https://mehdiouss.medium.com/membership) [## 通过我的推荐链接加入 Medium-Mehdi Aoussiad

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mehdiouss.medium.com](https://mehdiouss.medium.com/membership) 

**延伸阅读:**

[](/7-free-react-templates-you-can-use-for-your-projects-fb041304bf90) [## 7 个免费的 React 模板可以用于您的项目

### 真棒 React 模板和主题，你可以开始建立你的下一个项目。

javascript.plainenglish.io](/7-free-react-templates-you-can-use-for-your-projects-fb041304bf90) [](/github-repositories-to-prepare-for-javascript-interviews-47c012450681) [## 为 JavaScript 面试做准备的 10 个有用的 GitHub 库

### JavaScript GitHub 库帮助你赢得下一次面试。

javascript.plainenglish.io](/github-repositories-to-prepare-for-javascript-interviews-47c012450681) 

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***