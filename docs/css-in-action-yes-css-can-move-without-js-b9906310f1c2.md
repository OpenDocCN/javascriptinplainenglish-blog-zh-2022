# 🎬CSS 在行动:是的，CSS 没有 JavaScript 也能动！

> 原文：<https://javascript.plainenglish.io/css-in-action-yes-css-can-move-without-js-b9906310f1c2?source=collection_archive---------9----------------------->

## **过渡、变换和动画**

![](img/1759315785775827c9f5c6c932cb278e.png)

By FAM

你好👋

这一次，我们将只使用 CSS 来移动内容。是的，你没看错。我们不需要 JavaScript 来让 HTML 元素移动。

让我们给我们的故事加点动作吧！

# 过渡

CSS 中的转换有两个主要任务。确定要传输的 CSS 元素和效果持续时间。

让我们看看它像谁:

这里有一个`***div***` ，我们把它设计成一个带有`***width: 100px***`和`***height:100px***`的黑盒子:

在本例中，我们选择在覆盖`***div***`元素时，在`***width***` 属性上添加过渡效果。我们可以对其他 CSS 属性做同样的事情。你也可以给一些 CSS 属性添加效果，比如`***transition: width 2s, height 2s;***`。

**好吧，那** `**2s**` **呢？这表示过渡的持续时间:2 秒。**

我们可以做其他事情，比如通过使用属性`***transition-delay***`并给它秒来延迟过渡效果。我们也可以玩速度曲线，这是通过使用属性`***transition-timing-function***`完成的。该属性可以采用多种值:

*   `ease`:开始缓慢，然后快速，再慢慢结束的效果。
*   `linear`:从开始到结束速度相同的效果。
*   `ease-in`:慢速启动效果。
*   `ease-out`:结尾缓慢的效果。
*   `ease-in-out`:缓慢开始和结束的效果。
*   `cubic-bezier(n,n,n,n)`:让您在 [***三次贝塞尔***](https://cubic-bezier.com/#.17,.67,.83,.67) 函数中定义自己的值。

所有转换属性的示例(扩展和简写版本):

## 示例:

在这里找到源代码。

# 转换

现在，转变。这个 CSS 属性允许我们做更多令人兴奋的事情，例如在 2D 或 3D 中移动、旋转、缩放和倾斜元素。

以下是最常用的 2D 变换方法:

*   `translate()`
*   `rotate()`
*   `scaleX()`
*   `scaleY()`
*   `scale()`

对于 3D 变换，您可以使用以下方法:

*   `rotateX()`
*   `rotateY()`
*   `rotateZ()`

## 带变换的过渡示例

By web.dev

# 动画片

还有最后，最精彩的: ***动画*** 。是的，你只能用 CSS 动画元素。不需要 JavaScript！

以下是可用于此目的的 CSS 丰富属性:

*   `@ keyframes`:这个会在特定的时间从现在的风格逐渐变成新的风格。您需要给它命名，以便以后使用。这是用`@keyframes ***animationname*** { … }`完成的。
*   `animation-name`:这个属性允许我们使用自己创建的动画。本例中的`***animationname***` ***。***
*   `animation-duration`:顾名思义，它以秒为单位定义动画的持续时间。您必须指定它才能启动动画。否则，什么都不会发生。
*   `animation-delay`:指定延迟秒数，动画将在定义的秒数后开始。
*   `animation-iteration-count`:设置动画重复播放的次数。
*   `animation-direction`:设置动画的方向，向前(`animation-direction: normal`)、向后(`animation-direction: reverse`)或两个方向(先向前后向后:`animation-direction: alternate`，或先向后后向前`animation-direction: alternate-reverse`)。
*   `animation-timing-function`:设定动画的速度曲线。它采用与上面的变换[相同的值。](#11e0)
*   是一种速记属性，允许在一行中设置动画细节。它不像那样可读，但是它节省了 6 行代码。简短版本需要注释，以便其他开发人员理解代码的作用。

## 例子

By web.dev

# 知道这个非常重要

并非所有浏览器都支持所有属性。还有一些处于试验阶段的属性，所以要注意让你的网页在所有浏览器上(或者至少是用户或客户常用的浏览器上)看起来和反应都是一样的

我对这个问题的建议是:

## 使用供应商前缀

*   安卓:`***-webkit-***`
*   Chrome、iOS、Safari: `***-webkit-***`
*   火狐:`***-moz-***`
*   互联网浏览器:`***-ms-***`
*   歌剧:`***-o-***`

## 使用 CanIUse 工具

*   使用超级好的工具来确定浏览器对 CSS 属性的支持，如果支持的话，不需要为支持的浏览器添加供应商前缀。

今天就到这里，看阿雅🙋

如果您有任何问题或反馈，请点击评论或通过 LinkedIn 联系我— **我洗耳恭听！**

[**想请我喝杯咖啡吗？☕️**](https://www.buymeacoffee.com/fatimaamzil)

> 让我们为 2022 年打造一个更好的‘我们’！

## 了解有关 2022 年网络快车计划的更多信息:

I- [一般网络知识](https://medium.com/geekculture/2022-web-program-chapter-n-1-is-done-499fb0707220?source=your_stories_page----------------------------------------)

[II-网页框架:HTML](https://famzil.medium.com/your-html-essentials-69d9b2349355?source=your_stories_page----------------------------------------)

## 网页风格:CSS(当前章节)

*   [选择器(从基本到复杂)](/selectors-from-basic-to-complex-4f4f48316731?source=your_stories_page----------------------------------------)
*   [箱型](https://medium.com/geekculture/box-model-b67b40bb8930?source=your_stories_page----------------------------------------)
*   [排版](https://levelup.gitconnected.com/the-web-typography-eb92cdd9b534?source=your_stories_page----------------------------------------)
*   [定位](https://medium.com/geekculture/advanced-positioning-systems-in-css-90cf5689cb61?source=your_stories_page----------------------------------------)
*   [布局:柔性&网格](https://medium.com/geekculture/advanced-positioning-systems-in-css-90cf5689cb61?source=your_stories_page----------------------------------------)
*   [阴影、颜色和渐变](https://famzil.medium.com/css-beauty-de40e965c452?source=your_stories_page----------------------------------------)

> **转场&变换和动画**

*   响应式设计(媒体询问)

[](https://medium.com/geekculture/2022-web-program-is-launched-f38a3280af1a) [## 2022 网络计划启动！

### 改变来自心态和习惯

medium.com](https://medium.com/geekculture/2022-web-program-is-launched-f38a3280af1a) 

与想成为 web 开发人员的人分享该程序！这将有助于保持进步，并在旅途中互相帮助。

> 如果你喜欢我的文章， [**订阅**](https://famzil.medium.com/subscribe) 获取我的最新。如果你自己喜欢体验媒介，可以考虑通过[**注册会员**](https://famzil.medium.com/membership) 来支持我和其他成千上万的作家。它只需要每月 5 美元，它支持我们，作家，你也有机会用你的作品赚钱。当然，你可以随时取消会员资格。通过注册[这个链接](https://famzil.medium.com/membership)，你将直接用你的一部分费用来支持我，这不会花费你更多。如果你这样做了，万分感谢！

下面就让**在** [**中**](https://medium.com/@famzil/)**[**Linkedin**](https://www.linkedin.com/in/fatima-amzil-9031ba95/)**[**脸书**](https://www.facebook.com/The-Front-End-World)**[**insta gram**](https://www.instagram.com/the_frontend_world/)**[**YouTube**](https://www.youtube.com/channel/UCaxr-f9r6P1u7Y7SKFHi12g)**或**😉************

**[](https://famzil.medium.com/membership) [## 通过我的推荐链接——FAM 加入 Medium

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

famzil.medium.com](https://famzil.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***