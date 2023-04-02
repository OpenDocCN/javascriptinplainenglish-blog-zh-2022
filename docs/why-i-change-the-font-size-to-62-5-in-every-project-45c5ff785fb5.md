# 为什么我在每个项目中将字体大小改为 62.5%

> 原文：<https://javascript.plainenglish.io/why-i-change-the-font-size-to-62-5-in-every-project-45c5ff785fb5?source=collection_archive---------2----------------------->

## 帮助你简化计算的小开发技巧。

![](img/ef30ee973571e6f4679755cd9c0c2176.png)

Percentage sign GIF from [GIPHY](https://giphy.com)

# 语境

当我第一次开始用 CSS 编码时，我并没有真正注意其他的大小选项，如`rem`、`vw`、`vh`等。我只坚持传统的像素值，有时会使用百分比来设置像`div`的`width`到`100%`。

但是，当我开始更专业地学习和使用 CSS 时，我开始研究`rem` s 和`em`s。Kevin Powell 的这个[精彩视频](https://www.youtube.com/watch?v=N5wpD9Ov_To)是更深入了解它们的一个好来源。

# 问题是

然而，当你开始使用`rem` s 时，每次都很难计算它会有多少像素，反之亦然。就像你会得到一个使用像素的设计，但是你想使用`rem` s。

如果你正在使用类似 [Tailwind CSS](https://medium.com/u/d8c8c34e2236?source=post_page-----45c5ff785fb5--------------------------------) ( [*了解更多*](https://tailwindcss.com) )的东西，你真的不需要担心那么多计算。你可以只做一次，把它放在配置文件中，不用在每次需要使用它的时候计算它们。

另一方面，如果你只使用 CSS，SCSS，样式组件，或者基本上任何不为你做计算的东西。您可能需要使用特定的尺寸，每次您都必须将它从`rem` s 转换为`px`s，反之亦然。

有些人说你已经习惯了，但是当你可以通过写几行 CSS 来容易地解决这个问题时，为什么还要担心额外的事情呢？

# 解决方案

因此，避免计算的解决方案是在 CSS 重置文件中添加以下代码行。

```
html {
  font-size: 62.5%;
}
```

为什么 62.5%你问？因为 100% / 16px *10=62.5%

好了，现在让我们来分析一下，好吗？

我们将 100 除以 16，因为 16px 是浏览器的默认字体大小，所以我们得到 6.25，然后我们将它乘以 10，所以当我们试图从`rem`转换到`px`时，我们可以很容易地在脑海中计算出来。

例如，使用此设置，计算结果如下所示:

*   `1.6rem = 16px`
*   `2rem = 20px`
*   `0.4rem = 4px`
*   `10rem = 100px`

你明白了，拿你脑子里的任何数字，比方说`24px`除以 10，你在`rem`中得到你想要的结果，在这种情况下就是`2.4rem`。

但是等一下，我们还没有结束。在`html`中改变字体大小时，我们也会覆盖用户的喜好，这是非常糟糕的，因为这会扰乱用户的可访问性设置。

用户可能在他们的浏览器中将他们的`font-size`设置为`22px`，而我们作为开发者必须尊重他们的选择。但别担心，还有一个解决方案。

所以在`html`中设置`font-size: 62.5%`时，也应该在`body`中重置字体大小，如下所示:

```
html {
   font-size: 62.5%;
}body {
   font-size: 1.6rem;
   // ...
   // the rest of your resets
   //...
}
```

这解决了技术上由我们创造的问题。通过重置`font-size: 1.6rem`，我们可以说一切都应该回到浏览器的默认设置。

我们这样做不是为了缩小`html`中的字体大小来改变根字体大小，而是因为这个数字帮助我们更容易地将`rem`转换为`px`或者相反。

然而，如果我们不在正文中将其更改回`1.6rem`的话，这意味着我们只是缩小了根的大小，并且相当混乱了用户的偏好，甚至他们都不知道。

如果您更关心可访问性，您可以查看 [Aleksandr Hovhannisyan](https://www.aleksandrhovhannisyan.com) 的文章，他对可访问性做了更深入的探讨。

[](https://www.aleksandrhovhannisyan.com/blog/62-5-percent-font-size-trick/#respecting-a-users-font-size-preferences) [## 62.5%字号招数|亚历山大·霍芙汉尼斯扬

### 更新 05/10/2022:最初，本文结合了两个主题:为什么应该使用 rems 来调整字体大小，以及如何…

www.aleksandrhovhannisyan.com](https://www.aleksandrhovhannisyan.com/blog/62-5-percent-font-size-trick/#respecting-a-users-font-size-preferences) 

# 最后

你可能在某个地方见过这个把戏，或者你自己已经使用了一段时间，但你从未想过这会扰乱某人的偏好。

老实说，我也没有，直到有一天，我的一个朋友打开了我的一个项目，意识到他在设置中输入的字体大小不再有效。

只有到那时，我才能研究并找到亚历山大提供的解决方案，这也是本文的灵感来源。我只是想让更多的人知道如何使用这个酷把戏，没有任何陷阱。

如果这有帮助的话。考虑分享它，别忘了跟着我，这样你就不会错过我未来的文章。

[](https://medium.com/@kens_visuals/membership) [## 加入我的推荐链接 media-Ken Nersisyan

### 使用 Medium 释放您的潜力。现在就加入，阅读我和其他顶尖作家的文章。阅读、学习并变得更好…

medium.com](https://medium.com/@kens_visuals/membership) 

# 进一步阅读

[](/how-to-create-a-dark-mode-with-sass-scss-and-vanilla-javascript-e1c7835cf474) [## 如何用萨斯/SCSS 和香草 JavaScript 创建一个黑暗模式

### 试图在萨斯/SCSS 创建一个黑暗模式？完成本教程后，你将学会最简单的技术。

javascript.plainenglish.io](/how-to-create-a-dark-mode-with-sass-scss-and-vanilla-javascript-e1c7835cf474) [](/the-philosophy-of-chess-and-programming-3e435ef8bf14) [## 象棋和编程的哲学

### 我一直在思考国际象棋和编程之间的相似之处，下面是我的体会。

javascript.plainenglish.io](/the-philosophy-of-chess-and-programming-3e435ef8bf14) [](/how-to-master-problem-solving-as-a-programmer-d16a0b8780ab) [## 作为程序员如何掌握解决问题的能力

### 14 种练习解决问题的资源以及我是如何掌握技能的。

javascript.plainenglish.io](/how-to-master-problem-solving-as-a-programmer-d16a0b8780ab) [](/how-to-make-responsive-steps-progress-bar-with-vanilla-javascript-65dfa0515811) [## 如何用普通 JavaScript 制作响应式步骤进度条

### 你曾经想要建立一个完全自定义的步骤进度条吗？嗯，这是你一直在寻找的文章。

javascript.plainenglish.io](/how-to-make-responsive-steps-progress-bar-with-vanilla-javascript-65dfa0515811) [](/how-to-master-web-development-in-30-days-8f6d29237361) [## 如何在 30 天内掌握 Web 开发

### 什么是前端导师，它如何帮助我练习技能并走出教程地狱？

javascript.plainenglish.io](/how-to-master-web-development-in-30-days-8f6d29237361) 

# 让我们连接

[](https://twitter.com/kens_visuals) [## 在推特上关注我﹫kens_visuals

### 👨🏻‍💻👾

twitter.com](https://twitter.com/kens_visuals) [](https://github.com/kens-visuals) [## kens-视觉效果—概述

### 前端开发者| JS 爱好者|科技写手。kens-visual 有 67 个存储库。遵循他们的准则…

github.com](https://github.com/kens-visuals) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*