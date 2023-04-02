# 回应面试问题

> 原文：<https://javascript.plainenglish.io/react-interview-questions-one-must-know-f8fcda7d23df?source=collection_archive---------8----------------------->

## 第 1 章:React 必须知道的面试问题

![](img/cd4329497f41791e6947393d1287e9ec.png)

Photo by [Lautaro Andreani](https://unsplash.com/es/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个**开源 JavaScript 库**，主要用于设计和开发**可重用组件**。具有 JavaScript 背景的开发人员可以很容易地学习 React 并动手操作。React 是 web 开发人员和组织正在使用的最流行的前端技术。如果你正在准备 React 面试，下面是你必须知道的问题列表。

**1** 。**什么是** `**getSnapshotBeforeUpdate()**` **法？**

```
getSnapshotBeforeUpdate(prevProps, prevState) :
```

`getSnapshotBeforeUpdate()`方法属于组件生命周期的更新阶段。当组件由于任何状态/属性更改而被重新呈现时，这个方法将在 render()之后、dom 用最近的更改更新之前被调用。该方法返回的值将作为参数传递给`componentDidUpdate()`方法。`componentDidUpdate()`以`getSnapshotBeforeUpdate`命名。

**2。React 中的条件渲染是什么？**

当我们不得不从不同的组件中选择要渲染的内容时，条件渲染就出现了。在以下情况下，我们可能需要应用条件渲染

1.  从服务器获取数据并相应地设置变量。

2.在按钮/图标上应用可视条件。

3.处理用户事件

我们可以使用像‘if’这样的 JavaScript 操作符，让 React 决定呈现哪个组件。

**3。你将如何在功能组件中实现类似于** `**shouldComponentUpdate()**` **的功能？**

`ShouldComponentUpdate`可以在类组件中使用生命周期方法来检查我们是否需要重新渲染组件。这个方法检查当前和下一个状态和道具，如果它们相同，它将返回 false，如果它们不同，它将返回 true。默认为真。

我们可以在功能组件中使用钩子来实现 react 生命周期方法。对于`shouldComponentUpdate`，我们可以使用 useEffect 钩子。默认情况下，useEffect 将在每次更新/刷新时呈现。我们可以通过在数组中传递值来防止这种情况。该值将是组件输出改变的值(值=状态/道具变量改变值)。该数组将作为第二个参数传递给 useEffect。

在下面的代码片段中，假设 userId 最初是 100，在下一次重新呈现时，它仍然是 100，React 将比较 prev 和 next 值，因为它们相同，所以它将跳过 useEffect。如果该值不是 100，它将应用该效果。这就是如何实现类似`shouldComponentUpdate`的功能。

React useEffect Hook

**4。类组件和功能组件的区别是什么？**

在 React 中，组件是任何应用程序的构建块。组件是为代码可重用性而设计的。

## 1.类别组件:

在 react 中，类组件让我们使用 React 的生命周期方法。组件的安装、更新和卸载阶段可以在类组件中有效地处理。类组件在构造函数中声明了自己的状态变量。class 组件的第一个字母必须始终大写。他们有一个返回 HTML 的 render 方法。对于 React 版本< 16.8, class components were a must use if we need to manage the state and lifecycle methods in the components. Now with version 16.8, we have hooks that let us have state inside functional components also.

## 2\. Function Components:

Functional components are comparatively easy to code and handle. They are nothing but the JavaScript functions which return JavaScript XML. The functional component name must start with an upper case letter. React version > = 16.8 已经引入了钩子，通过它我们可以在函数组件内部拥有状态。我们还可以使用钩子在功能组件中实现类似 react 生命周期的功能。

**区别:**

**类组件:**

*   他们有自己的国家。
*   它们从反应组分延伸。具有返回 HTML 的 render 方法。
*   因为它们有自己的状态，所以也被称为有状态组件。

**功能组件:**

*   没有状态。(可通过使用挂钩实现)
*   它们是简单的 JavaScript 函数。没有呈现方法。
*   功能组件只是接受道具和渲染，因此它们也被称为无状态组件。

Class Component snippet

Functional Component Snippet

**5。什么是 setState()方法，为什么使用它？**

在类组件中，我们在构造函数中声明了状态变量。我们可以通过`this.state`访问它们。当涉及到更新状态变量时`setState()`就出现了。`setState()`方法更新状态值并重新呈现组件。它本质上是异步的。

你可以用`this.state.variable_name = UpdatedValue`更新状态变量，但是使用 setState 更新状态总是更好，因为要重新渲染。这确保了组件将总是具有更新的值。

如果在错误的生命周期方法中使用 setState 的重新呈现功能，可能会导致类似无限循环的问题。例如，如果我们试图在 render()中使用 setState，它将触发重新渲染，并将进入无限循环，导致服务器崩溃。

如前所述，setState 本质上是异步的，因此我们不能确定 setState 方法中使用的`this.state`值。例如，如果我们有一个被频繁点击的 like 按钮，我们不能保证最近的 like 计数值。在这种情况下，我们可以向 setState 传递一个回调函数，该函数将在状态更新后被调用，我们将获得最新的 likes 计数值。

setState Example

**6。“==”和“===”有什么区别？**

*   ==被称为相等运算符，而===是严格的相等运算符。
*   ==运算符在比较之前进行类型转换。===运算符不会进行类型转换。

**7。** `**this.state.name = “abc”**` **与** `**this.setState({name:”Abc”})**` **的区别。什么时候使用这两种方法？**

在这两种情况下，我们都试图用值 **abc** 来更新状态变量 **name** 。根据两种情况下的代码，它会将状态变量更新为 abc，但这里的关键区别是，当我们使用 setState 方法时，它会使组件**重新呈现**。
setState 导致协调，即它将使用更新后的值重新渲染组件树。因此，如果我们试图在`this.state`之前更新状态，组件将没有更新的状态，因此将导致状态不一致。使用 **setState** 进行状态更新始终是一个最佳实践。

8。状态和道具的区别？

**State:** State 是一个保存组件内部数据的 JavaScript 对象。换句话说，可以说状态是一个在组件内部携带数据的变量。不能在组件外部访问它。通过使用`this.state`可以访问状态变量。使用 `this.setState()`可以修改状态变量。

**道具:**道具也是保存数据的对象，但是与状态不同，道具可以在不同的组件之间共享。在 react 中，一切都是一个组件，当我们想要在这些组件之间进行通信时，我们可以使用 props。道具是只读的。道具是不可变的，所以我们不能修改组件内部的道具。

**区别:**

**状态:**

*   状态是可变的。
*   不能在组件外部访问状态。
*   状态可用于共享组件内部异步更新的数据。

**道具:**

*   道具是不可改变的
*   可以在组件外部访问 Props。
*   Props 用于不同组件之间的数据共享。

本文到此为止。如果你喜欢这篇文章，请不要忘记查看其他文章！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*