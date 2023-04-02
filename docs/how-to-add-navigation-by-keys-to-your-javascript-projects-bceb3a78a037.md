# 如何在您的 JavaScript 项目中添加“按键导航”

> 原文：<https://javascript.plainenglish.io/how-to-add-navigation-by-keys-to-your-javascript-projects-bceb3a78a037?source=collection_archive---------7----------------------->

## 关于如何在您的项目中实现“**按键导航**功能的教程。

![](img/f55ae9eb2c35adabb62ec757dc90402f.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你有没有想过一些网站和 JavaScript 项目是如何嵌入“**导航键**”并认为这很酷的？嗯，你来对地方了。今天我将教你如何在你的项目中实现“**按键导航**”功能。所以让我们开始吧。

# 什么是“按键导航”？

首先，我们要知道这里所说的“**按键导航**”是什么意思。这里的“按键导航”是指如果我们按下键盘上的某个键，我们就可以执行某个功能。比如我们按下键盘上的 R 键，它重启游戏或者重新加载网站等等。

# 如何实现“按键导航”？

为了实现这个奇妙的特性，我们将使用以下语句:

```
window.addEventListener("keydown", key_nav);function key_nav(event) {
    var key = event.key;
}
```

首先，我们将向名为“keydown”的窗口添加一个事件侦听器，这意味着无论何时按下任何键，该函数都会触发。确保将事件侦听器添加到窗口中，否则它将无法工作。现在`key_nav`是函数的名字。你可以给它起任何你喜欢的名字。将`event`作为参数添加到函数中。

在函数内部声明一个变量并将`event.key`初始化为它的值。我已经把它命名为`key`，但是你可以给它起任何你喜欢的名字。`event.key`表示事件发生时按下了哪个键。

现在你想知道`event.key`长什么样。要知道这个写`console.log(key)`在函数里面。你应该把你用来存储`event.key`的变量的名字写在`key`的位置。现在，无论你何时按下任何键，它都会在控制台中输出该键的`event.key`。这将有助于您了解`event.key`对于您想要添加导航的按键的外观。

现在，在这个函数中，使用`if`条件来指定您想要使用的每个键的函数——就像在下面的笔的第 684 行中，我将导航添加到箭头按钮来导航井字游戏网格，并指定如果您按下回车键，该函数将放置十字形或圆形:

下面是如何添加“**按键导航**这一惊人的功能，它一定会让你的项目更加出色。请随意使用我上面的笔，我希望你会喜欢这篇文章。

再见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***