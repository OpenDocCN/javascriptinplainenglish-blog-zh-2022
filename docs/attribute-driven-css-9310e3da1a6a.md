# 属性驱动的 CSS

> 原文：<https://javascript.plainenglish.io/attribute-driven-css-9310e3da1a6a?source=collection_archive---------1----------------------->

## *避免用 JavaScript 切换 CSS 类*

![](img/08e2ea2e3d2316ecf298f1388f8ee032.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在开发网站或 web 应用程序时，我们有时会面临动态内容样式的挑战。有一种常见的方法可以解决这些问题，但今天我想向您展示另一种方法，并解释为什么它更好。

## 动态内容样式

我说的“动态内容样式”是什么意思？每当 JavaScript 干扰你的风格时。以下是一些例子:

你会如何设计手机导航？它看起来会像这样吗？

```
<nav class=`nav {navOpened ? 'open' : ''}`>
```

解决方案的外观取决于您使用的语言，但它通常看起来与任何语言都相似。我经常看到这种模式。另一个例子是像这样有条件地隐藏:

```
<div class=`some-cool-class {toggled ? 'd-show' : 'd-hidden'}`>
```

请注意，*公开*或 *d-show* 风格可能会做同样的事情。当然，这也可能是直接切换/添加样式以避免出现类名，但这同样糟糕，如果不是更糟糕的话。

这种技术在 body 元素中也很常见。例如，当 DOM 完全加载时，人们用它来附加一个特定的类，当网站滚动时，或者当一个模态打开时，用它来锁定滚动。

```
<body class=`{loaded ? 'loaded' : ''} {scrolled ? 'scrolled' : ''} {scrollLock ? 'scroll-lock' : ''}`>
```

这有几个问题:

1.  条件样式和类很难阅读，尤其是当你组合了几个静态和动态类的时候。
2.  JavaScript 规定了元素的外观(关注点分离)。
3.  你最终要么对同一个类使用多个类，要么用一个类来管理它们(开放类对 d-hidden/d-show)。我通常看到的最糟糕的情况是两者兼而有之。

那么，什么是更好的解决方案呢？

## 属性驱动的方法

这种方法将 HTML 数据和 aria 属性用于样式元素。例如:

```
<nav class="nav" aria-expanded=`{navOpened}`>
```

现在，您可以在 CSS 中使用 aria 属性作为选择器:

```
[aria-expanded='true'] {
  /* ... */
}
```

是的，这可能并不总是一个好主意。你不能简单地用 aria-hidden 隐藏任何元素(尽管你可以隐藏任何没有表示作用的 aria-hidden 元素)，而且你可以说这也混合了分离(a11y 和样式)。如果您想要严格分离，您可以利用数据属性:

```
<nav class="nav" aria-expanded=`{navOpened}` data-expanded=`{navOpened}`>
```

和 CSS:

```
[data-expanded='true'] {
  /* ... */
}
```

下面是之前 body 元素的例子:

```
<body data-loaded=`{loaded}` data-scrolled=`{scrolled}` data-scroll-lock=`{scrollLock}`>
```

为什么更好？

1.  JavaScript 只控制属性，不控制类名。
2.  数据属性可以作为变量名的附加描述(参见上面的数据扩展和 navOpened 名称的例子，它们在一起阅读时是有意义的)。因此，它增加了可读性。
3.  任何数据扩展的元素都将接受特定的样式；你会有不同的机制来避免混合通用和专用的解决方案。
4.  您不必为 open 或 hidden 这样的状态定义类名；它们是属性。

就这些了，伙计们。
感谢您的阅读。

你对此有什么看法？之前有条件添加类名吗？你如何解决可读性问题？

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***和******T48 不和**T52**