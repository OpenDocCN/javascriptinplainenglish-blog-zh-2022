# React Portals:一种在 React DOM 上将子对象与其父对象分开的方法

> 原文：<https://javascript.plainenglish.io/react-portals-a-way-to-separate-a-child-from-its-parent-on-a-react-dom-cc893ec83264?source=collection_archive---------8----------------------->

## 了解什么是 React 门户，何时需要它们，以及如何使用它们。

![](img/976635e484e64f533349ca2ffcca22e6.png)

Image created by the author on Canva

# 什么是 React 门户？我们什么时候需要它们？

React Portal 是一种将子组件呈现为 DOM 节点的方法，该节点位于实际父组件的层次结构之外。简单来说，它是 React DOM 中另一个地方的入口。

当我们在 React 中创建一个组件时，它遵循已经声明的 DOM 层次结构。例如，我们创建一个名为 ***的子组件*** ，其父组件为 ***父组件*** 。在 React DOM 中，*父组件*将是父组件，而*子组件*将嵌套在*父组件中。*查看下面的示例代码，理解 DOM 上父子组件的嵌套。

```
***// Child component*** function Child() {
    return (
        <h2> This is a child component. </h2>
    )
}***// Parent component*** function Parent() {
    return (
        <div className="container">
            <Child/>
        </div>
    )
}***// How they will be nested onto the DOM.*** <div class="container">
    <h2> This is a child component. </h2>
</div>
```

在这种情况下，DOM 考虑在父组件中声明子组件。现在，如果我们想在另一个 DOM 节点下呈现子组件，该怎么办呢？当我们需要使用 React Portals 为我们的子组件创建到另一个节点的入口时，就是这种情况。

在这里，你可能会想，为什么我要在别处呈现我的组件呢？据说将 React 门户与 ***模态、工具提示和对话框*** 一起使用是一个很好的实践。这是因为我们希望它们与声明它们的组件分开，这样父类的样式就不会影响它们。假设*父*组件有一个 ***溢出*** 样式的 ***隐藏*** ，那么*子*组件也将被隐藏。为了使我们的子组件不被隐藏，我们需要它独立存在，通过为子组件使用一个门户，这变得可能。

使用 React Portal 的另一个好例子是使用模态。考虑一个 z 索引作为样式给出的父组件。不能为模态子组件分配更高的 z 索引，因为它遵循父组件的样式。

# 如何实现 React 门户？

看下面 React Portal 的语法。第一个参数是我们希望在 DOM 上从其父组件中分离出来的任何子组件，比如元素、字符串或片段。第二个参数将是任何目标节点或 DOM 中我们想要添加子节点的元素。

```
ReactDOM.createPortal(child, targetNode)
```

这里，我们将使用***document . body***作为目标节点。但是，您可以使用任何 DOM 节点或元素的 class 或 id 属性。请看下面 React 门户实现的例子。我已经重构了上面使用的子组件和父组件，以便清楚地理解它们的区别。

```
import ReactDOM from 'react-dom'***// Child component*** function Child() {
    return ReactDOM.createPortal(
        <h2> This is a child component </h2>,
        document.body    
    )
}***// Parent component*** function Parent() {
    return (
        <div className="container">
            <Child/>
        </div>
    )
}***// How they will be nested onto the DOM.*** <div class="container"></div>
<body>
    <h2> This is a child component </h2>
</body>
```

在子组件中实现 React 门户后，可以在 DOM 树中清楚地看到差异。父组件的

元素现在变成了空的，子组件的

## 元素被直接包装到了标签中。

通过这样做，我们应用于*容器*类的任何样式都不会应用于子元素，子元素现在可以单独使用它们自己的样式。

# 关于 React 门户的重要经验

在使用 React Portal 时，有必要了解它只修改浏览器中的 DOM 树，而不会改变 React 树。换句话说，对于 React，子元素

## 仍然是父组件的子元素。

尽管这个子节点可以在 DOM 树中的任何位置，但它的行为就像 React 树的普通 React 子节点一样，与在 DOM 树中的位置无关。在子元素中触发的事件仍然会传播到包含 React 树中的祖先，即使这些元素不是 DOM 树中的祖先。这个概念被称为 ***通过门户冒泡的事件。*** 同样，React 仍然拥有对节点和元素生命周期的控制权。

# 结论

本文的目的是理解 React 门户及其用例。我已经给出了一个例子来创建一个我们需要使用 React 门户的场景。我希望这篇文章能帮助您理解 React 门户。请跟随我阅读更多类似这样有趣的文章。

[](https://medium.com/@kardaniyagnik/membership) [## 通过我的推荐链接加入 Medium-Yagnik Kardani

### 阅读雅格尼克·卡尔达尼(以及媒体上成千上万的其他作家)的每一个故事。如果你喜欢我的文章，请用我的…

medium.com](https://medium.com/@kardaniyagnik/membership) [](https://www.buymeacoffee.com/kardaniyagnik) [## Yagnik Kardani 正在创建帮助他人成长的技术学习材料。

### 你好👋，我是一名媒体方面的技术作家。我喜欢学习并帮助他人在软件开发和云计算方面成长…

www.buymeacoffee.com](https://www.buymeacoffee.com/kardaniyagnik) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*