# 反应原生:修复闪烁字段格式

> 原文：<https://javascript.plainenglish.io/react-native-finding-a-fix-for-flickering-field-formatting-dc1923e97cc?source=collection_archive---------3----------------------->

## 在 React Native 中对 TextField 输入应用动态格式会触发难看的闪烁——以下是解决方法。

![](img/e7345831e6577dacee091ad3a6769717.png)

Photo by [Zach Vessels](https://unsplash.com/@zvessels55?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 场景

我们试图做的是**构建一个 TextField，它可以对用户输入应用某种格式或其他限制**。

一个非常常见的用例是格式化货币金额:如果我的应用程序要显示一个美元值作为用户输入，我可能希望输入“1–0–9–9”，并让我的输入显示“$10.99”。如果用户输入一个非数字字符，我希望这个击键被忽略。同样，如果用户试图添加第三个小数位。无论输入什么，您都希望文本被格式化为美元和美分的货币值。

另一个用例可能是限制输入，只允许某些字符。假设我们希望用户为用户名提供一个只包含字母数字字符的字符串:如果用户键入“joe_bob19！!"，我们的输入应该会自动将输入限制为“joebob19”。任何其他字符都应该被自动剔除。

那么我们如何在 React Native 中实现这个用例呢？让我们尝试几种方法，看看它们是如何工作的。

# 最初的尝试

如果您是从零开始处理这个用例，有两种通用的方法可以用来解决这个问题。至少，这些是我在找到解决方案之前尝试过的想法。

**方法#1** :实现一个 **onChange** 处理程序来格式化或处理用户输入，并改变传回到 **TextInput** 中的值。它看起来大概是这样的:

`<TextInput value={name} onChange={value => setName(format(value))} />`

这种方法将允许您获取完整的用户输入字符串，对其进行处理以格式化或过滤掉不需要的字符，然后在 **TextInput** 上将它重新设置。这里没有显示完整的代码，但是我们显然使用了某种状态管理，比如用`React.useState`表示`name`和`setName`，我们还有一些`process`函数，它可以接受任何字符串并返回它的“修正”版本。

**方法#2** :向按键处理程序添加一些逻辑，并尝试拒绝导致不良输入的事件。您可以尝试一个 **onKeyDown** 处理程序，并尝试在事件到来时对其进行处理。如果事件导致无效输入，您可以拒绝该事件。

这种方法在使用案例中会有一些限制，因为它不允许您格式化整个字符串，但是它仍然允许您解决“不可用字符”的情况。

这两种方法在 React for web 中都是可行的(做了一些小的改动)，但不幸的是，这两种方法都不能在 React Native 中很好地工作！

# 问题是

这些方法的问题是，因为 React Native 是，嗯，*原生的*，我们最终会与原生文本输入组件发生冲突。在 React for web 中,“文本输入”实际上是 React 完全控制的 DOM 的一部分，这使得上述两种方法都可行。然而，在 React Native 中， **TextInput** 组件是一个真正的本机组件，它在本机端消耗键盘事件并更新自身，不受 React Native 的完全控制。只有在组件更新之后*我们的 hander 代码才会运行。*

![](img/d07e635f102baa479c7bf339d3c91ee4.png)

Flickering & flashing in a ReactNative TextInput

因此，上面的方法#1 有点“工作”,但有一个主要的不良视觉副作用:当(不良)输入首先被本机组件立即显示，然后被 JavaScript“修复”时，输入值闪烁不定。

方法#2 根本不起作用，因为在 JS 方对发生的事情有发言权之前，事件已经被本地组件使用了。

不幸的是，这种闪烁是 React Native 的一个[已知问题，这两种提议的方法都不可行。那么我们如何解决这个问题呢？](https://github.com/facebook/react-native/issues/24585)

# 修复

这个问题的解决方案并不明显，但是相当简单。我们将使用两个，而不是使用一个**文本字段！第一个将是“input”**文本字段**，它将接受用户输入*，但不会显示。*第二个将是我们的“显示”**文本字段**，它将显示*但不接受用户输入*。**

通过将显示字段精确地放在输入字段的上面，我们甚至可以保持正确的光标显示。最终结果如下所示:

![](img/fe13a353df8648552692e8997406ae5f.png)

The fixed TextField inputs

如果你仔细观察上面的动画，你会发现当用户输入被格式化时，你会看到一个*微小的*光标移动。我认为这是一个可以接受的折衷，但是如果你不喜欢，你可以移除光标或者实现你自己的光标行为。

关于这种方法的实现有几点注意事项:

*   显示字段是关于定位的“主”文本字段——使用 **onLayout** 处理程序获取其位置，然后相应地绝对定位输入文本字段，以获得正确的光标行为
*   如果你把显示文本域直接放在另一个之上，你还需要在显示域上添加 **pointerEvents="none"** 来允许用户与底层输入交互。
*   你应该用**颜色:“透明”**使输入文本字段“隐藏”，而不是像**不透明度:0** 那样的另一种方法，因为这将使文本不可见，但仍会显示光标。

# 结论

React Native 是跨平台应用程序开发的一个很好的框架，但是“JavaScript 加 Native”的方法有时会导致棘手(并且令人讨厌)的情况，就像本文中描述的那样。不过，只要有点创造力，我们通常可以找到这些问题的解决方案，并继续做重要的事情。

[*Jonathan*](http://medium.com/@jonnystartup) *在创业公司大&小有超过 20 年的工程领导经验。在业余时间，他在做一个文档自动化平台，*[*【Imagepipe.co】*](http://imagepipe.co/)*。*

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**