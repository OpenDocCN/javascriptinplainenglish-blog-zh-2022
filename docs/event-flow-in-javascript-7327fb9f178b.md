# JavaScript 中的事件流

> 原文：<https://javascript.plainenglish.io/event-flow-in-javascript-7327fb9f178b?source=collection_archive---------7----------------------->

![](img/32b9894e4b72ae103d15c2d6ca26c302.png)

Photo by [Sandro Katalina](https://unsplash.com/@sandrokatalina?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/neon?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在这篇文章中，我们将通过例子来理解 JavaScript 中的事件以及事件在 JavaScript 中是如何流动的。所以，不要浪费太多时间，让我们开始吧。

# JavaScript 事件

JavaScript 事件只不过是来自基于用户动作的输入设备的信号。它可以是鼠标点击、键盘上的按钮按压或者甚至仅仅是鼠标移动被认为是事件。

事件流或事件传播是在 DOM 节点上触发事件的顺序。根据事件流的方向，有两种类型的事件:

1.  **事件冒泡**
2.  **事件捕捉**

# 事件冒泡

这是一种事件传播类型，事件首先在最里面的目标元素上触发，然后在目标元素的父元素上连续触发，直到到达最外面的 DOM 元素。

流向:**子** **→父**

event bubbling example

在上面的例子中，您可以看到有 3 个嵌套的 div。当你点击子 div(点击我！)你会注意到在`console.log`中，首先打印的是`child` get，然后是`parent`和`grandparent`。这里的事件从子节点流向父节点，即使事件只在子 div 上执行。事件冒泡是浏览器使用的事件传播的默认行为。

# 事件捕获

这是一种事件传播类型，事件首先被最外面的元素捕获，然后在目标元素的子元素上连续触发，直到到达最里面的 DOM 元素。

流向:**上级→下级**

event capturing example

在上面的代码示例中，你会注意到当我们点击子元素`Click Me!`时。在运行子事件处理程序时，首先运行最顶层的 div `grandparent`事件处理程序，然后运行子事件处理程序。由于捕获不是事件传播的默认模式，我们必须显式地允许事件捕获。我们可以通过将处理程序选项`capture`设置为`true`来实现这一点，如下所示

```
element.addEventListener(..., {capture: true})

// or, just "true" is an alias to {capture: true}
element.addEventListener(..., true)
```

为了阻止事件传播到不同的 DOM 节点，我们可以使用`event.stopPropagation()`方法。在 DOM 节点上执行 Stop propagation 方法将阻止冒泡和捕获事件传播。应该小心使用方法，因为改变事件传播的默认行为可能会在我们的 web 应用程序中导致一些意想不到的结果。下面是使用`event.stopPropagation()`的代码片段。

even stop propagation example

在上面的代码中，`child`事件处理程序正在执行`event.stopPropagation`方法，这将中断事件流，因此只有`child`将被打印在`console`中。

感谢您阅读这篇文章。欢迎在评论区分享你的想法。快乐阅读！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，*** *和****不和*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***