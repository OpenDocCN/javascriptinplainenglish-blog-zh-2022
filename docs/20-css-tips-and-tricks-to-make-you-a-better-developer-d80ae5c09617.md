# 20 多个 CSS 技巧和窍门，让你成为更好的开发者

> 原文：<https://javascript.plainenglish.io/20-css-tips-and-tricks-to-make-you-a-better-developer-d80ae5c09617?source=collection_archive---------4----------------------->

## 让你成为更好、更灵活、更快的开发者的顶级 CSS 技巧和诀窍。

![](img/749778de23489c6ee78bc540ad9bb566.png)

# 前言

**修改输入占位符样式、多行文本溢出、隐藏滚动条、修改光标颜色、水平居中和垂直居中。**多么熟悉的场景！前端开发者几乎每天都会和他们打交道，这里有 20 个 CSS 招数，大家看看吧。

# 1.解决图像 5px 间距问题

你是否经常有图片底部多余 5px 间距的问题？不急，这里有 4 种方法可以解决。

![](img/45f5b52b321cdb6150ddb865ba12660a.png)

picture 5px spacing

**解决方案 1:将 font-size: 0 设置为父元素**

CodePen demo

**解决方案 2:将显示:块设置为 img**

CodePen demo

**解决方案 3:将垂直对齐:底部设置为 img**

CodePen demo

**解决方案 4:将行高:5px 设置为父元素**

CodePen demo

# 2.元素高度与窗口高度相同

如何让元素和窗口一样高？

CodePen demo

# 3.修改输入占位符样式

第一个是修改过的，第二个不是。

![](img/d741de27c4d2c7d6961361b338a1b9f4.png)

CodePen demo

# 4.使用“:非”选择器

除了最后一个元素之外，所有元素都需要某种样式，使用 not 选择器将非常容易。

**如下图:最后一个元素没有下边框。**

![](img/7a19aecdf3528aca2a9a90d6bb937716.png)

CodePen demo

# 5.使用 flex layout 智能地将元素固定在底部

当内容不够时，按钮应该在页面底部。当有足够的内容时，按钮应该跟随内容。当你有类似的问题时，使用 flex 实现智能布局！

![](img/f433587b8f8ffcbc976c573d6320b438.png)

fixed bottom

CodePen demo

# 6.使用“脱字颜色”修改光标颜色

有时需要修改光标的颜色。现在是脱字符颜色显示时间。

![](img/fd454ed98fdb30cda6e4234e5b3c6dd1.png)

CodePen demo

# 7.移除 type="number "末尾的箭头

默认情况下，输入 type = "number "的末尾会出现一个小箭头，但有时我们需要去掉它。我们做什么呢

**如下图:第二个去掉了，第一个没有。**

![](img/25590c7523d4db63d3fb25f63f73a0f3.png)

Remove the arrow at the end of type=”number”

CodePen demo

# 8.“大纲:无”删除输入状态行

当输入框被选中时，默认情况下它会有一条蓝色的状态线，可以使用 outline: none 来移除。

**如下图:第二个输入框被移除，第一个没有。**

![](img/5788a0fa6b48739c4ee0f752ba1e423d.png)

# 9.解决 iOS 滚动条被卡住的问题

> *在苹果手机上，经常会出现滚动时元素卡顿的情况。此时只有一行 CSS 会支持弹性滚动。*

# 10.画三角形

![](img/502f27d9160d629c6867426990248e56.png)

triangle

# 11.画小箭头

![](img/b3d6089b69be251040a81ca2e1040e36.png)

Draw small arrows

# 12.图像适合窗口大小

vw 与填充

![](img/873eb0eeea63af7d034fafdeca57a6e4.png)

vw vs padding

# 13.隐藏滚动条

第一个滚动条是可见的，第二个是隐藏的。

**这意味着容器可以滚动，但是滚动条是隐藏的，就像它是透明的一样。**

![](img/cc889e714969d80bd9ec8a8f35733d2a.png)

Hide scroll bar

# 14.自定义选定的文本样式

![](img/7b48363f76488cecb03f518089e72865.png)

Customize the style of text selection

# 15.不允许选择文本

第一个可以选择，第二个不可以。

![](img/de813452862cdc04370ef41819ae9701.png)

Disable selection of text

# 16.水平和垂直居中元素

![](img/972ae83ad0ebb85a571cc8837936377a.png)

Horizontal and vertical centering

# 17.单行文本溢出时显示省略号

![](img/7e22ae80bec8b7a58ff51d44b5db57c8.png)

Single line text

# 18.多行文本溢出时显示省略号

![](img/25166628b52f6171b4c415c346ae0921.png)

Multi-line

# 19.清除浮动

> 这是一种古老的布局方式，现在大多数移动终端都不使用。

如下所示，外层的高度不会塌陷，这就是使用 clearfix 类的原因

![](img/0613192d9c6b0ea7b396640e1d3c38ff.png)

Clear float

# 20.使用“过滤器:灰度(1)”使页面处于灰色模式

一行代码将使页面处于灰色模式。

![](img/c46fcd0dd27e99a98216618d27077572.png)

filter:grayscale(1)

```
body{
  filter: grayscale(1);
}
```

# 结局

我是胖鱼。我有 6 年的编程经验，喜欢前端，写作，交友，期待和你成为好朋友。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。***