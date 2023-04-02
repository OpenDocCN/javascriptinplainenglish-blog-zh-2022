# 我在 CSS 中学到的 3 件事可能对你有益

> 原文：<https://javascript.plainenglish.io/3-things-i-learned-in-css-that-might-benefit-you-d99b6e11ebef?source=collection_archive---------8----------------------->

![](img/b79c644e0f08d0fb20bfdede05e78d55.png)

Photo by [Caleb Woods](https://unsplash.com/@caleb_woods?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cat-with-laptop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

首先，我为因为我的考试而休息道歉，其次，我想感谢我的观众，他们甚至在我休息的时候都支持我。我原以为当我打开 medium.com 的时候会有 30 个左右的追随者，但是看起来只有一两个。对此我非常感激。现在让我们进入文章。

# 1)网格布局中的宽度

大约一个月前，我在学习 CSS 中的网格布局。当我讲到如何跨越超过两行或两列的网格项目时(我想你现在已经知道了`grid-column-start`、`grid-column-end`、`grid-row-start`和`grid-row-end`属性)，我制作了一个网格并在其中放置了一些网格项目。然后，我开始编写 CSS 来使一个网格项目跨越两列。我做的一切都很好，但它仍然不会跨越两列。我又试了几次，但还是没有成功。

我停止了学习网格，但是今天(写这篇文章的那天)我再次开始编写 CSS 来使一个网格项目跨越两列，但是仍然没有用。在观察代码时，一个想法闪过我的脑海，“如果我为网格项设置的`width`属性可能会阻碍这个过程呢？”。我迅速删除了设置`width`属性的语句，瞧！成功了。结果呢？似乎当我们在 CSS 中为一个元素设置一个`width`属性时，它甚至会在 grid 中保持这个宽度。

所以小费呢？不要对网格项目使用`width`属性。这将使他们不再令人敬畏和幻想。我今天学到了它，我会做更多的实验，我会告诉你我将来是否会在网格中学到一些东西。

# 2)相对单位

相对单位(%)、rem、em、ch 等。)是 CSS 中的单位，其大小取决于父元素的大小。例如，如果一个`div`的`font-size`被设置为`20px`，那么如果我们将该 div 的一个子元素的`font-size`设置为`50%`，那么它的`font-size`将是`10px`的 50%。

相对单位是响应式网站设计的经验法则(制作一个网站，使元素在位置和大小上适合所有类型的屏幕尺寸，包括在 PC 或笔记本电脑上调整浏览器窗口的大小)

一个好的网站显然是一个有反应的网站。这是网站开发者和客户都知道的。所以学习和练习相对单位会让自己受益匪浅，喜欢很多。

# 3)每个开发人员都需要的技巧

这个提示是每个开发者都需要的提示。秘诀的总结就是“不要自焚，按照自己的风格工作”。让我解释一下。你是人类。你需要休息。你不是一台机器。即使是机器，在长时间连续工作后也需要休息。你有其他的职责，其他人也有一些权利，你需要履行这些职责，比如和家人在一起，和朋友聊天。这就是“不要烫着自己”的意思。现在对于“以你的风格工作”，每个人都有自己的风格，他们感到舒服。是的，他们比其他人更好，但他们也需要你的风格。编程不是制作最好的程序，而是寻找问题解决方案的过程。这和制作网站是一样的。是的，你应该尽最大努力使网站比别人做得更好，但有时即使使用最好的风格也可能适得其反。因此，永远遵守提示，“不要烧伤自己，以你的方式工作”

以下是我在 Web 开发和编程之旅中学到的 3 件事，会让你受益匪浅。我希望你在你的编程之旅中能成功实现你的目标，我希望你喜欢这篇文章，也会喜欢我以后的文章。最后，我想感谢你对我的支持。

谢谢你，

再见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***