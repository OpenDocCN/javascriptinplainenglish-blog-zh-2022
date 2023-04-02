# 当软件开发人员谈论意大利面条式代码时，他们指的是什么？

> 原文：<https://javascript.plainenglish.io/what-do-software-developers-mean-when-they-talk-about-spaghetti-code-d66e7c71c736?source=collection_archive---------7----------------------->

![](img/4d89d7e1ec8130546555be9244b0dbe6.png)

Photo by [Homescreenify](https://unsplash.com/@homescreenify?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

意大利面条式代码与函数的长度关系不大，与混合职责关系更大。一个函数可能很好，有时更长。

根据您的偏好，您还可以指定，例如，没有哪一行可以比 80 列更全面—这导致格式化后的行数明显更多，但是您可以同时并排读取两个文件(例如，对于代码审查或在比较查看器中很有用)

对我来说，意大利面条代码是指当它“从背后穿过胸部”或者当一个类或模块是“万能的”

例如，混合业务和视图逻辑。当数据模型描述时，显示的是 UI 而不是实际数据。

副作用(相对于“纯函数”)真的很糟糕:一个函数或方法声称做 A，但同时也做 B 和 C。

阅读意大利面代码不足以理解它；你必须调试它。你无法在脑海中描绘和想象他要做什么。相反，你必须继续读回程序的其他部分，记住那里刚刚发生了什么，然后回到原点，考虑可能的含义。整个事情往往可以深入几个层次，“进进出出”

虽然好的代码可以映射到一个示意图上，并且关系/交互会像电路一样流动，但是意大利面条式代码更像一盘意大利面条，而不是电路板或电路板。

如果你想知道一片意大利面去了哪里(它“做了什么”)而不把它全部撕开，你应该准备好你的手术设备，并且一丝不苟。

由于开发人员有时缺乏对意大利面条式代码的概述，代码变得独立。它通常会执行太多不必要的操作(例如，由于不必要的副作用)，最终的软件通常性能非常差，不可维护(“工作，最好不要再碰它”)。

例如，我不知道这是我的 Android 手机上的中型文本编辑器还是后台的什么东西，但输入最后几行纯粹是一种痛苦——一个输入的字母需要很多秒才能进入文本，在这个过程中，光标像疯了一样来回跳动——有 10 秒的延迟——突然我在文本的中间而不是结尾写了，我想在那里写点什么。

我把这归咎于意大利面条代码。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*