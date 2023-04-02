# 你可能不知道的 5 个 HTML 属性

> 原文：<https://javascript.plainenglish.io/5-html-attributes-that-you-probably-dont-know-of-c8947de3a1bb?source=collection_archive---------10----------------------->

在 HTML 中，属性和标签一样重要

![](img/a057917bedddc14317c86c0a327631a8.png)

Photo by [Siora Photography](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

不久前，我写了一篇[文章](https://betterprogramming.pub/5-html-tags-you-might-not-know-were-a-thing-1ef8843c855)，分享了一些我以前不知道的 HTML 标签。如果你想了解这些标签，你可以点击[这里](https://betterprogramming.pub/5-html-tags-you-might-not-know-were-a-thing-1ef8843c855)。

你可能听说过 **HTML 是关于标签的，标签是关于属性的**。就像我们有一些隐藏的 HTML 标签一样，我们也有一些你可能没有听说过的 HTML 属性。在这篇文章中，我们将讨论其中的一些。

## 1.接受

如你所知，HTML 允许我们创建输入，你可以上传你的文件。除此之外，HTML 属性 accept 用于上传输入，以指定文件类型或用户可以上传到服务器的唯一格式。

```
<input type="file" accept=".jpg, .png">
```

上面提到的输入元素将只接受扩展名为 jpg 和 png 的文件。

## 2.多重

当 Boolean **multiple** 属性被设置时，表示表单控件接受一个或多个值。对`email` 和`file` 输入类型以及`<select>`有效，用户选择多个值的方式由表单控件决定。

如果设置了 **multiple** 属性，表单控件可能会根据类型有不同的外观。浏览器提供的本地消息传递因文件输入类型而异。

当电子邮件输入类型设置为多个时，用户可以输入零个(如果不需要)、一个或多个逗号分隔的电子邮件地址。

```
<input type="email" multiple name="emails" id="emails">
```

如果指定了 **multiple** 属性，则该值只能是格式正确的逗号分隔的电子邮件地址列表。列表中的每个地址的任何尾随和前导空格都将被删除。

当文件输入类型设置为**多个**时，用户可以选择一个或多个文件。用户可以以他们的平台允许的任何方式(例如，通过按住 Shift 或 Control，然后点击)从文件选取器中选择多个文件。

```
<input type="file" multiple name="uploads" id="uploads">
```

当省略该属性时，用户只能通过`<input>`选择一个文件。

`<select>`元素的 **multiple** 属性表示从选项列表中选择零个或多个选项的控件。否则，`<select>`元素是一个允许您从选项列表中选择单个`<option>`的控件。当指定 multiple 时，大多数浏览器将显示滚动列表框，而不是单行下拉列表框。

## 3.[计] 下载

当用户点击超链接时，HTML **download** 属性用于下载元素。仅在设置了`href` 属性时使用。属性的值将是下载文件的名称。如果该值不存在，则使用原始文件名。它出现在`<a>`和`<area>`元素中。

```
<a href="img.png" download="img.png">Download Now</a>
```

通过点击由上述 HTML 元素生成的**立即下载**链接，用户将能够下载**img.png**文件。

## 4.翻译

**translate** 属性是一个枚举属性，它指定当页面被本地化时，元素的可翻译属性值和文本节点子元素是否应该被翻译。

它可以是下列任何值:

*   如果字符串为空或`yes`，当页面被本地化时，该元素应该被翻译。
*   `no`，表示该元素不应该被翻译。

> 虽然不是所有的浏览器都认可这个属性，但是它受到自动翻译系统如 Google Translate 的尊重，也可能受到人工翻译工具的尊重。因此，网站作者使用这个属性来识别不应该翻译的内容是非常重要的。

```
<p translate="no">Medium</p>
```

## 5.海报

HTML **poster** 属性用于在下载视频或用户点击播放按钮时显示图像。如果未指定此图像，视频的第一帧将用作海报图像。这就像一个 YouTube 缩略图。

该属性与`<video>`元素一起使用。

```
<video poster="thumbnail.jpg" controls>
    <source src="file.mp4" type="file/mp4">
</video>
```

这就是这篇文章的内容。我希望你今天学到了一些新东西。想看更多这样的文章，敬请期待！

感谢阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*