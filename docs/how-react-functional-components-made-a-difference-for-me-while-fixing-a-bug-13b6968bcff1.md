# 在修复 Bug 时，React 功能组件如何对我产生影响

> 原文：<https://javascript.plainenglish.io/how-react-functional-components-made-a-difference-for-me-while-fixing-a-bug-13b6968bcff1?source=collection_archive---------7----------------------->

## 什么是功能组件？功能组件是返回 React 元素的函数。

![](img/25a8ed36d58269022d5a924027bca5bc.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

功能组件可以理解为返回 React 元素的函数，该元素接收表示组件属性的参数`props`。

在 React 16.8 之前，也就是没有 React 钩子，功能组件只作为 UI 组件，其输出完全由参数`props`控制，没有其状态或业务逻辑代码，是纯函数。功能组件没有实例，没有生命周期，被称为无状态组件。

React 钩子出现后，钩子可以用来赋予功能组件状态和生命周期，所以功能组件也可以作为业务组件使用。

在开发过程中，功能组件比类组件更容易使用，以下两点感受最深:

*   不用上课，不用担心烦人的这个指点问题。
*   高复用性使得提取常见的，编写自定义钩子替换高阶组件变得容易。

函数组件和类组件有一个非常重要的区别:**函数组件捕获用于渲染的值**。

我是在遇到一个 bug 的时候才知道这个区别的，在解决这个 bug 的过程中明白了这个区别的意义。

BUG 场景是这样的:有一个输入框和输入内容后，点击按钮进行搜索，在搜索的时候，首先请求的是一个接口，我们得到一个类型，然后用这个类型和输入框的值来请求搜索接口。这里用代码简要描述:

上面的代码逻辑看起来没有错，但是 QA 给我指出了一个 bug。在输入框中输入要搜索的内容后，点击搜索按钮开始搜索，然后在输入框中快速输入内容。结果，搜索界面`getList`报告一个错误。

检查原因，发现`getType`接口`getType`和搜索接口`getList`接受的参数`val`不一致。

在排查过程中，我很疑惑。很明显`val`在两个请求中都读取了`this.state.inpValue`的值。然后，我的同事指示我改用功能组件来解决这个 bug。

换成功能组件后，再试一次，没有报错，bug 修复。后来我发现，事件的状态和道具在功能组件中获得的值，就是事件被触发那一刻，用于页面渲染的状态和道具的值。

点击搜索按钮时，`val`的值就是此时输入框中的值。无论输入框后面的值如何变化，都不会捕捉到最新的值。

那为什么可以在类组件中获取最新的状态值呢？关键是在类组件中，状态是通过`this`获得的，`this`始终是最新的组件实例。

在类组件中更改它也可以解决这个 bug。这些变化如下:

当搜索事件`handleSearch`被触发时，输入框`this.state.inpValue`的值被存储在`inpValue`变量中，随后的事件使用输入框的值来获取`inpValue`变量。输入框中的后续输入不会影响`inpValue`变量的值，除非搜索事件 handleSearch 被再次触发。这个修改也可以解决这个 bug。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----13b6968bcff1--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----13b6968bcff1--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----13b6968bcff1--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----13b6968bcff1--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----13b6968bcff1--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----13b6968bcff1--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***