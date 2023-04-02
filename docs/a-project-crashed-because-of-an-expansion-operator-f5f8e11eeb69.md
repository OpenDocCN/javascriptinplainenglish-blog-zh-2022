# 一个项目因为一个扩展操作符而崩溃

> 原文：<https://javascript.plainenglish.io/a-project-crashed-because-of-an-expansion-operator-f5f8e11eeb69?source=collection_archive---------4----------------------->

## 当一个已经在线稳定运行了一年多的项目突然崩溃。

![](img/0904920f6d6be78e054ed22f4d693634.png)

Photo by [Fili Santillán](https://unsplash.com/es/@filisantillan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 前言

在一个周末的晚上，我躺在沙发上看电视，享受闲暇时光。

突然，一条紧急消息说一个 bug 需要尽快修复。

● [Boss]着急地说:“Fatfish，你的代码有问题。用户的页面崩溃了。现在反馈给客服。请看一看。”

●[我]很惊讶:“不应该。这个代码上线一年多了，一直没有问题，最近也没改。”

大家好。我在分享一个准确有趣的故事。前几天，一个在线稳定运行了一年多的项目突然崩溃了。查了一下，发现这段代码的提交者是我自己，但是仔细考虑了一下，没有发现问题。

# 发现问题

代码简化删除后，留下这样一段代码可能会有问题。

`getValuesById`是根据`id`得到一个数组。这里由于业务的特殊性，需要合并两个阵列。其实合并数组的方法有很多种。当时，我选择了使用`push`。

乍一看，这段代码没有任何问题，编写方法也很普通。应该不会出现页面崩溃问题。另外，我进行过多次本地验证，都可以正常工作。

稳定运行一年多的项目代码可能出现问题的原因是什么？唯一的变化是时间。时间会改变什么？是因为项目运行时间长了，这里的数据量变大了，导致栈爆炸吗？

所以我很快模拟了这段代码在有大量数据问题时的操作:

栈居然爆炸了，然后页面崩溃了！

![](img/b16745f4c1cc9b8fb612e58326fadbb6.png)

为什么这个代码会爆？是因为`push`还是分机操作员？为了找出根本原因，我对这个 ES6 代码进行了一次 Babel 转换。结果是:

你可以看到这段代码最终变成了`push apply(values, newValues)`。

在查阅了相关资料后，我了解到，如果以上述方式调用`apply`，可能会超出 JavaScript 引擎参数的长度，并且这里传入的多余参数在不同的 JavaScript 引擎中会有不同的表现。由于这种限制，一些引擎会抛出异常，甚至导致参数丢失。

我的上帝，是这样的。谁能想到一个小小的延伸操作符和`push`会有这样的副作用？这是否意味着，当传入的参数超过限制时，在所有函数中使用扩展运算符也会有这样的副作用？经过测试，我找到了答案。

# 解决问题

有许多方法可以合并数组。我们可以改变一个合适的方法。

1.  使用`concat`合并。

2.使用扩展运算符(更常用)进行合并。

3.循环推送。

*更内容于*[](https://plainenglish.io/)**。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。跟随我们登上*[](https://twitter.com/inPlainEngHQ)*[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***和******T50***对成长黑客感兴趣？*查看 [***电路***](https://circuit.ooo/) ***。*T69******