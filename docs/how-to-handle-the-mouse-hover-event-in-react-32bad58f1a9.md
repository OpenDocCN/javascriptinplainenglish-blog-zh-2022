# 如何在 React 中处理鼠标悬停事件

> 原文：<https://javascript.plainenglish.io/how-to-handle-the-mouse-hover-event-in-react-32bad58f1a9?source=collection_archive---------2----------------------->

## 解决 React 中缺少 onHover 事件处理程序的问题

![](img/b8e5bd957d691fbde6f697452d36b884.png)

Photo by [Rebekah Yip](https://unsplash.com/es/@rebekahyip?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

与您可能想到的相反，React 中没有`onHover`事件处理程序。这并不意味着 React 阻止您处理鼠标悬停事件。相反，React 为您提供了`onMouseEnter`和`onMouseLeave`事件处理程序。这两个可以用来在 React 中很容易地实现鼠标悬停逻辑，在这里，您将了解开始使用它们所需的一切。

遵循本教程，学习如何实现以下结果:

A CodeSandbox live demo to show the HoverableComponent in use

# React 中的 onHover 事件处理程序

如果熟悉 jQuery，应该知道`[hover()](https://api.jquery.com/hover/)`函数。这允许您将一个或两个处理程序绑定到一个或多个 DOM 元素。当鼠标指针进入选定的 DOM 元素时，执行第一个处理函数，当鼠标离开 DOM 元素时，执行第二个处理函数。

考虑到 React 中事件处理程序的命名约定，比如`onClick`、`onFocus`和`onSubmit`，您可能会想到一个`onHover`事件处理程序。然而，HTML `[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)`规范不包括悬停事件。因此，**`**onHover**`**事件处理程序在 React** 中不存在。**

**因此，如果您想在 HTML 元素的 React 组件中实现悬停逻辑，您必须寻找以下状态:**

*   **鼠标进入 HTML 元素**
*   **鼠标离开 HTML 元素**

**这正是 jQuery 在`hover()`函数中所做的事情。因此，您可以使用以下两个[鼠标事件](https://reactjs.org/docs/events.html#mouse-events)处理程序在 React 中的 HTML 元素上实现悬停逻辑:**

*   **`onMouseEnter` →当鼠标指针移动到 React HTML 元素上时，它调用相关的回调函数。**
*   **`onMouseLeave` →当鼠标指针移出 React HTML 元素时，它调用相关的回调函数。**

**现在让我们来学习如何使用它们。**

# **在 React 中使用 onMouseEnter 和 onMouseLeave 处理鼠标悬停**

**让我们用一个例子来看看如何处理鼠标悬停事件。最常见的例子是在鼠标悬停时改变 HTML 元素的样式。然而，这可以完全在 CSS 中处理，并且不需要 React。所以，这不是一个好例子。**

**这里你会看到一个组件的例子，它的状态根据悬停状态而改变。具体来说，下面的`HoverableComponent`显示或隐藏基于鼠标悬停在`div`上的消息:**

**The HoverableComponent definition in JavaScript**

**正如您所看到的，要获得想要的结果，需要通过`[useState()](https://reactjs.org/docs/hooks-state.html)`钩子使用 React 状态。当鼠标进入`div`元素时，调用`onMouseEnter`事件处理程序，将`showMessage`变量设置为`true`，并显示“Hello，World！”显示消息。相反，当鼠标离开`div`元素时，调用`onMouseLeave`事件处理程序，将`showMessage`变量设置为`false`，并显示“Hello，World！”消息被隐藏。**

**因此，当鼠标悬停在`div` HTML 元素上时，`showMessage`布尔变量会更新，消息会相应地显示或隐藏。请注意，这里展示的`HoverableComponent`与本文开头的现场演示中使用的组件相同。**

**瞧啊！这就是如何在 React 中处理鼠标悬停事件。**

# **结论**

**在本文中，您了解了 React 没有附带`onHover`事件处理程序。这意味着如果你想在 React 中处理鼠标悬停事件，你需要一个特殊的方法。具体来说，您可以使用`onMouseEnter`和`onMouseLeave` React 事件处理程序轻松实现悬停逻辑，这里您通过一个简单的例子看到了如何实现。**

**感谢阅读！我希望这篇文章对你有所帮助。请随意留下任何问题、评论或建议。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***