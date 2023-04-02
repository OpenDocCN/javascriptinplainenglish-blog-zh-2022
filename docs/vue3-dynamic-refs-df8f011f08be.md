# Vue3 动态参考

> 原文：<https://javascript.plainenglish.io/vue3-dynamic-refs-df8f011f08be?source=collection_archive---------1----------------------->

## 重用面向函数的方法

![](img/59e72bfe5c144e35fa209ef036aa666b.png)

# 方案

假设你有多个有图标的可点击区域。无论您在父元素中的什么位置单击，都希望输入字段成为焦点。

# 问题

根据您点击的位置，`$event.target`会发生变化。这意味着你要么用一个聪明的方法找到预期的目标，要么采取优雅的方法。

# Vue2 溶液

最优雅的方法是定义一个 ref 并访问与被点击的元素相对应的 ref。

在 Vue2 中，这将如下所示。

Vue2 Dynamic Refs

# Vue3 问题

如果你正在使用 Vue3 组合 API，你会注意到实现这种行为并不是非常明显。

方法不再能够访问包含组件中定义的所有引用的对象。所以你可能最终会满足于一个不那么优雅的解决方案。然而，你不必。

# Vue3 解决方案

解决办法很简单。使用属性值为引用的对象。然后，您可以将您的模板更新为如下所示。

Vue3 Dynamic Refs

# 奖金:一个更好的方式来定义裁判

而不是一遍又一遍的写 ref。你可以写一个方法来定义数组中的引用。由于我在使用 Lodash，所以我做了一些类似的事情。

Lodash Define Vue Refs

现在我可以这样重写我的`inputs`定义:

Vue3 defineRefs Usage

# 结论

您可以使用动态引用，而不是使用事件目标来聚焦元素。这样做允许您重用事件处理程序。

[](https://devmap.org/membership) [## 通过我的推荐链接加入 Medium-Wade Zimmerman

### 阅读 Wade Zimmerman(以及 Medium 上成千上万的其他作家)的每一个故事。您的会员费直接支持…

devmap.org](https://devmap.org/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***