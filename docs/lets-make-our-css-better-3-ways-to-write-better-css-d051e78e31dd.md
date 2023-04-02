# 让我们把 CSS 做得更好——写更好的 CSS 的 6 种方法

> 原文：<https://javascript.plainenglish.io/lets-make-our-css-better-3-ways-to-write-better-css-d051e78e31dd?source=collection_archive---------4----------------------->

## 通过实现这些方法更有效地编写 CSS。

![](img/d968fa73363de9345773062b3cdef26b.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/css?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

与十年前相比，世界已经取得了很大的进步，正如所料，编程领域也取得了进步。现在我们只需要 HTML 和 CSS 就可以制作出动态漂亮的网站。因此，每个 web 开发人员都应该了解高级 CSS 的新技术。除此之外，一个优秀的 web 开发人员知道如何编写维护良好的 CSS。所以现在在这篇文章中，我将谈论提高你的 CSS 多样性的方法和习惯。请记住，没有人是完美的，你将永远需要实践和磨练你的技能。

# 1.组织您的代码

这是每个 CSS 编码者必须养成的习惯。这对团队合作(你可能会遇到很多次)和你自己都有好处。你应该定期组织你的代码。

通过组织代码，你将能够发现错误和对你不利的代码。所以在我看来，比起普通的书面代码，你应该更喜欢组织良好的代码。

# 2.为你的利益使用选择器

选择器是 CSS 中的一个重要特性，对于一个想成为能够编写最先进的 CSS 的程序员的人来说，它的专业知识是不可忽视的。此外，一个好的 web 开发人员知道如何以最佳方式利用必要的选择器。

如果你问我，一个知道使用 CSS 选择器的真正方法的开发者可以不使用 JavaScript 来做事情。所以你应该经常练习你对 CSS 选择器的掌握。

# 3.不要使用不必要的线

这个技巧意味着，当您可以不用额外的代码行来编写代码时，您不应该使用额外的代码行。例如，请参见下面的 CSS。

```
p.box {
    margin: 10px;
}div.area {
    margin: 10px;
} 
```

在上面的代码中，您可以看到`p.box`和`div.area`都将 margin 设置为 10px。我们可以一次性设置，而不是使用不同的行。

```
p.box, div.area {
    margin: 10px;
}
```

看看有多大区别。这样，你的代码也将被组织起来，易于维护。此外，这也将减少网站的总负荷。因此，没有必要这样写代码，因为每个人都有自己的风格，但它肯定会帮助你。

# 4.使用相对单位

在当今的网站世界中，网站响应越快，就越成功。响应式意味着它可以响应所有尺寸的屏幕。你可以通过两种方式实现这一点。第一个是使用相对单位。相对单位(雷姆、埃姆、%等。)是其尺寸或长度依赖于另一尺寸或长度的单位。例如，参见下面的代码。

```
div.box {
    font-size: 30px;
}div.box span {
    font-size: 50%;
}
```

在上面的代码中，将`div.box`的`font-size`设置为 30px。现在，在下一行中，我们将`div.box`中`span`的`font-size`设置为 50%。这意味着跨度的`font-size`将是父元素`div.box`的`font-size`的 50 %。所以字体大小会是 30px 的 50 %会是 15px。

相对单位依赖于父元素的属性值。您可以使用相对单位来设置属性的值，使其随着父元素的属性值的变化而变化。

# 5.使用媒体查询

媒体询问在开发响应网站中非常重要。媒体查询用于根据屏幕大小和其他因素指定元素的属性。媒体查询一开始很难理解，但是在响应式 web 开发中，如果不是最重要的，也是非常重要的。

使用媒体查询肯定会提升你在响应式 web 开发中的竞争力，无论屏幕大小如何，你的网站都将是动态的、宏伟的。

# 6.使用短手

在 CSS 中，大多数情况下每个属性都有一个简写属性。请参见以下代码

```
p.box {
   margin-left: 2px;
   margin-right: 4px;
   margin-top: 5px;
   margin-bottom: 0px;
}
```

在上面的代码中，我们将各种边距的值设置为`p.box`元素。现在，通过使用`margin` short hand，我们可以在一行中初始化这四个属性。

```
p.box {
   margin: 5px 4px 0px 2px;
}
```

看看有多大区别。CSS 中的许多属性都有简写，如填充、边距、边框等。此外，通过使用短手，网站的总负荷减少。除此之外，它还保持了代码的组织性。所以你应该总是用短手。

这里有 6 种方法或习惯，它们一定会让你成为一名优秀的 web 开发人员，并帮助你更有效地编写 CSS。请记住，每个人都喜欢并有自己的风格，编程或编码的最终目标应该是在一天结束时充满乐趣。

我希望你将在你的编码之旅中取得成功，我希望你喜欢这篇文章，如果你不介意，请留下一个提示来支持我。很有帮助:-)

谢谢你，

再见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***