# 简单的黑客与反应元素和 JSX

> 原文：<https://javascript.plainenglish.io/why-react-elements-position-matters-1e50aa239560?source=collection_archive---------5----------------------->

![](img/a50640f2819f5b2b1421844f3ab9c038.png)

没有完美的软件。作为开发人员，我们必须时刻意识到未来的变化。明白了这一点，React 有一个强大的组合模型，很容易交换组件。因为我们可以创造性地选择如何定位和交换我们的组件，所以会有不同的结果，每种结果都有自己的好处，这取决于上下文。最好，在本文中，我们将讨论定位组件的不同方法，了解它们，并明智地选择合适的方法。

# 目录:

*   **什么是 React 元素？JSX 运输公司？:**为什么？稍后我们将在此基础上解释接下来的概念。
*   **渲染行为:**React 元素在渲染过程中的作用，浪费渲染是如何发生的？
*   **常量元素如何帮助优化渲染**

# **什么是 React 元素？JSX 运输公司？**

![](img/7819d6a514b0ce4666188d12b953a53a.png)

一个 **React 元素**是由一个**组件**返回的。它是一个虚拟描述组件所代表的树节点的对象。

等等，什么？我没有看到组件返回的任何对象？不就是 **JSX** 吗？

让我解释一下！

诚然，Component 返回 JSX，但 JSX 是一种 JavaScript 无法直接读取的特殊语法。相反，它需要 transpilers 将其转换成 createElement 调用，这只是 JavaScript 普通对象。根据你的栈，传输可以通过 **Babel** 或者 **TypeScript** 来完成。这就是为什么你总是要用`import React from ‘react’`来写 JSX，因为它需要运行`React.createElement`，所以`React`需要在范围内。从 React 17 开始，有了一个新 JSX 变换——不再需要导入，如果你好奇，可以在这里阅读更多。

如果你想测试一些特定的 JSX 是如何转换成 JavaScript 的，你可以试试[巴别在线编译器](https://babeljs.io/repl)。

## 多个孩子

React 不限制一个组件的子组件数量，它会被编译成:

在这一点上，我们学习漂亮的 JSX 和元素的想法，这将支持即将到来的事情。

# **渲染行为:**

渲染是一个 React 发现布局树应该是什么样子的过程，它发生在挂载和更新的时候。在更新期间，执行协调以收集新树和旧树之间的差异，一旦组件被标记为需要更新，React 将重新渲染其所有子组件，即使这些子组件保持不变。在这方面，浪费的渲染出现，可能会花费很多精力，可能会减慢我们的应用程序。

在 GIF 中，我建了一个例子，其中`Component A` > `Component B` > `Component C` > `Component D`，A 是 B 的父组件，以此类推。由于 React 中的渲染行为，当组件 A 被标记为需要重新渲染时，所有子组件也会重新渲染，如果子组件没有更改，它也不会在意。它从父节点开始跟踪并 diff 到其子节点，所以重新渲染 B 只触发 C & D，A 不在其中。

有时，其中一个孩子很慢，我们不希望在慢的组件上进行不必要的重新渲染。优化一个东西有两种方法，要么让它跑得更快，要么跳过工作。在 React 中，大多数优化都是关于跳过工作的。React 提供了 3 个主要方法来实现这一点: **React。PureComponent** ， **shouldComponentUpdate** ， **React.memo** 。我就不赘述了，你可以在[我之前的博客](/react-native-why-props-references-break-optimizations-79c463ca0723)里看到。相反，利用对元素和 JSX 的理解，我们得到了另一个简单的方法，没有使用上述 3 种方法。

# **常量元素如何帮助优化渲染**

看看这个例子，我们有一个`SlowComponent`，它将渲染延迟了 **1 秒**，还有一个`TestCon`显示`count`，它在按下时增加计数。

让我们来看看有`SlowComponent`和没有`SlowComponent`两种情况的区别:

正如我们所见，当我注释掉`SlowComponent`时，我们的反例运行顺利；否则，`SlowComponent`会将 SlowComponent 的渲染延迟 **1 秒**，这也会影响到`TestCon`。为什么？正如我解释的，上面的渲染行为，`TestCon`中的`setCount`也触发其子组件重新渲染，`SlowComponent`延迟 1 秒，作为父组件的`TestCon`必须等待`SlowComponent`完成，最终提交到树。

## 修复

常见的修复是**协同状态**，以及我上面提到的 3 种方法。**共置状态**意味着将`count`状态和使用它的组件包装成一个单独的组件。

`WrapperComponent`是新添加的组件，用它包装`count`状态和布局。这样做可以防止`SlowComponent`被重新渲染，因为现在更新被标记在`WrapperComponent`处，而不再是`TestCon`处，所以它只关注`WrapperComponent`及其子节点。

等等！如果有另一个`MondayComponent`需要使用计数，或者一个新的`ParentView`也需要使用计数:

哦不！在这种情况下我们不能使用共存状态，我们需要`TestCon`处的`count`将它传递给`ParentView`和`MondayComponent`。

一个简单的技巧就能让`SlowComponent`飞起来。

提升内容意味着将`SlowComponent`传递给`TestCon`作为道具，孩子只是一个道具，所以`props.children`或`props.renderSlow`或任何你喜欢的名字都无关紧要。这样做如何防止`SlowComponent`重新渲染？

为了看起来更好，我稍微简化了这个例子，所以现在只有`View`和`SlowComponent`。

我们用上面学到的关于 **JSX** 和 **createElement** 来描述两种写作方式。

对于第一种情况，每次`TestCon`重新渲染时，`React.createElement(SlowComponent)`都会被调用，因此它在渲染之间总是不同的，所以 React 只是重新渲染它，这解释了为什么其他子组件也会被重新渲染。

对于第二种情况，不管`TestCon`重新渲染多少次，`props.children`总是相同的，因为基于它被定义的位置，它是一个常数，并且它的引用是相同的。

引用在 React 生态系统中起着重要的作用，它影响大多数优化方法，因为 React 内部使用浅层比较。

因此提升内容会阻止内容的重新呈现。请注意，在现实世界的例子中，有些情况下，您希望将子对象与父对象一起重新渲染，或者跳过重新渲染子对象以提高性能，这取决于具体情况。所以明智地选择:

```
<TestCon><SlowComponent/></TestCon> and use props.children
==> when you want skip SlowComponent renderingotherwise, use SlowComponent directly for re-render along with parentconst TestCon = ()=>{
 return(
   <View>
    <SlowComponent/>
   </View>
 )
}
```

总的来说，这是优化组件的众多方法中的一个简单的方法，只需将它们放在周围即可。适当地使用它，不同的情况需要不同的方法。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*