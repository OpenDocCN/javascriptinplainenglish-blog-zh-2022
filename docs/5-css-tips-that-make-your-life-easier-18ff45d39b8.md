# 让你的生活更简单的 5 个 CSS 技巧

> 原文：<https://javascript.plainenglish.io/5-css-tips-that-make-your-life-easier-18ff45d39b8?source=collection_archive---------7----------------------->

## 为你的下一个项目准备一些实用的 CSS 技巧。

![](img/7b2be8e8c79ab0bf85288e48db078a35.png)

Photo by [Thought Catalog](https://unsplash.com/@thoughtcatalog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我是那些定期检查新的 CSS 技巧的人之一，只是为了发现虽然它们肯定很有趣，但在我的日常编程生活中它们通常是无用的。所以，我想:为什么不自己写一篇关于 CSS 技巧的文章呢？开始了。

## 1.使用 CSS 选择任何子对象

第一个 CSS 技巧很简单，但是非常方便。假设您想要选择一个 div 的子元素。下面是一个标记示例:

```
<div class="my-div">
  <span></span>
  <span></span>
  <span></span>
</div>
```

您可以像这样选择它们:`.my-div > span`。这将选择所有属于 span 元素的`.my-div`的直接子元素。但是，如果从 span 切换到 div 呢？或者更糟，如果我们有像这样的混合元素呢:

```
<div class="my-div">
  <span></span>
  <div></div>
  <p></p>
</div>
```

如果想要选择任何子元素，只需使用通配符选择器:`.my-div > *`。我经常读到不应该使用通配符选择器。我不能同意那件事。你可以自由使用，但一定要谨慎使用。我喜欢将它与儿童选择器结合使用，因为不会有太多问题。

注意`.my-div > *`和`.my-div *`的区别。

## 2.使用当前系统字体

现在大部分网站的系统字体看起来都比较好。它们还提供了本地的外观和感觉。因此，继续使用它们并不坏，还能节省使用谷歌网络字体的额外流量(以及与 GDPR 的麻烦)。

在很长一段时间里，我们必然会使用这样的东西:

```
font-family: -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui, helvetica neue, helvetica, Cantarell, Ubuntu, roboto, noto, arial, sans-serif;
```

它被称为“系统字体堆栈”

然而，在相当长的一段时间里，有一种更简单的方式来访问系统字体，并且浏览器支持非常好:

```
font-family: system-ui;
```

 [## “系统-用户界面”|我可以使用 HTML5、CSS3 等的支持表格吗

### “我可以使用吗”提供了最新的浏览器支持表，以支持桌面和移动设备上的前端 web 技术…

caniuse.com](https://caniuse.com/?search=system-ui) 

我很少看到这个被使用；我经常看到长的字体堆栈字符串。那么，为什么不在你的下一个项目中尝试一下呢？

## 3.重置元素的样式

你曾经做过类似的事情来重置元素的样式吗？

```
div {
  background: none;
  border: none;
  color: inherit;
  outline: none;
  padding: 0;
}
```

有更好的办法！

```
div {
  all: unset;
}
```

太棒了。全浏览器支持！[https://caniuse.com/?search=all](https://caniuse.com/?search=all)

## 4.非跳动底部边框

当突出显示一个活动或悬停的元素时，我们有时会使用边框，就像这样:

```
<div class="my-element">...</div>
<div>
  test
</div><style>
  .my-element:hover {
    border-bottom: 1px solid black;
  }
</style>
```

然而，如果事先没有边界，我们会得到“跳动的边界”效果。为了避免这种情况，我们过去使用了一些“技巧”。例如，在焦点上，您可以使用轮廓而不是边框。

*说明:轮廓不是盒子模型的一部分；因此，它不会“推动”周围的其他元素。例如，轮廓的宽度对其周围的元素没有影响。*

但是大纲解决方案在上面的例子中不起作用，因为大纲没有`outline-bottom`属性。

一个简单的“破解”方法是在非悬停状态下给元素添加一个透明边框。然而，还有另一个解决方案。大多数情况下，您可能需要它来放置某种高度固定的盒子。这就是你可以利用`box-sizing`的地方。

```
<div class="my-element">...</div>
<div>
  test
</div><style>
  .my-element:hover {
    border-bottom: 1px solid black;
  }.my-element {
    height: 18px;
    box-sizing: border-box;
  }
</style>
```

现在，这是从它的高度中减去边框的大小；因此，元素不会变得更高。相反，它的内容会缩小。因此，您不能总是使用这种解决方案。在上面的例子中，如果你将边框尺寸增加到——比如说——5px，那么你就会明白我的意思了。

为了您的方便:

然而，对于 1 或 2px 的简单边框，尤其是在向文本添加填充时(按钮和导航链接通常都有)，这种解决方案可以派上用场。

## 5.使用:where()减少您的 CSS

有时，我们希望对不同元素的子元素应用相同的样式。考虑以下 CSS:

```
.a > span,
.b > span,
.c > span {
...
}
```

这可以用`:where()`来写:

```
:where(.a, .b, .c) > span {
...
}
```

但是，请注意浏览器支持。尤其是 Safari 可能会成为一大亮点。

 [## "哪里" |我可以使用 HTML5、CSS3 等的支持表

### “我可以使用吗”提供了最新的浏览器支持表，以支持桌面和移动设备上的前端 web 技术…

caniuse.com](https://caniuse.com/?search=where) 

就这些了，伙计们！

想要更多吗？留下一个关注或使用鼓掌功能来告诉我你想要更多的东西！

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**