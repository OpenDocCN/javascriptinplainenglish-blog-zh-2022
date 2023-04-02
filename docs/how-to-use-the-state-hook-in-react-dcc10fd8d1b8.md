# 如何在 React 中使用 useState 钩子

> 原文：<https://javascript.plainenglish.io/how-to-use-the-state-hook-in-react-dcc10fd8d1b8?source=collection_archive---------9----------------------->

## 了解 React 中最常用的钩子之一。

![](img/518f70ba9024beb4be2ec3abfe330abe.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个由组件组成的世界。

组件本身维护它们自己的“状态”。

你可能会问，什么是“状态”？

状态只是一个普通的旧 JavaScript 对象，用来记录组件中包含的数据。

该数据可能保持不变，或者由于用户执行的某些操作而更新。

从 React 16.8 开始，React 中的类和功能组件都可以维护状态。

由于 React 团队[更倾向于使用功能组件](https://reactjs.org/docs/hooks-intro.html#motivation)而不是类组件，让我们看看状态是如何在功能组件中管理的。

# 功能组件中的状态

假设您想跟踪用户点击按钮的次数。

您可以维护一个“count”变量作为组件的状态变量来跟踪点击次数。

每次用户单击按钮时，都要更新状态中的“count”变量。

让我们看看语法是什么样子的:

```
import "./styles.css";
import { useState } from "react";export default function App() {
  const [count, setCount] = useState(0);
  const updateCountHandler = () => {
    setCount(count + 1);
  };
  return (
    <div className="container">
      <button onClick={updateCountHandler}>Click</button>
      <p>No. of clicks: {count}</p>
    </div>
  );
}
```

在上面的代码片段中，组件使用语句维护其状态:

```
const [count, setCount] = useState(0);
```

让我们从右到左理解这段代码中发生了什么:

首先，我们看到使用参数 0 调用了 useState 挂钩。

“useState”是 React 提供的内置挂钩。

传递给它的参数是我们希望在第一次呈现时用来初始化状态的值。因为“计数”是一个数字，我们希望它从零开始。提供初始值完全是可选的。

转到赋值操作符的左边，我们看到一个奇怪的带有方括号的语法，即，

```
const [count, setCount]
```

上面的语法可能看起来令人困惑，所以让我来解释一下。

当我们用初始值调用 useState 钩子时，它返回一个数组。

该数组包含我们的状态变量“count”和一个更新计数变量“setCount”的函数。

下面的代码片段相当于方括号代码片段。

```
 const countState = useState(0);

  const count = countState[0]; // count state variable  
  const setCount = countState[1]; // count state updater function
```

如果在一个组件中有多个状态要维护，那么这个语法很快就会变得混乱，很难跟踪。

这样，使用方括号语法(即数组析构)来避免编写样板代码就变得很方便了。

此外，您可以随意命名“count”和“setCount”。在你的状态更新函数前加上前缀“set ”,后跟它正在更新的状态的名称，这是一个很好的做法，这样可以理解被操作的状态和负责它的函数。

转到 updateCountHandler。

您可以看到，它正在通过调用 useState 提供的“setCount”函数来更新计数，并将值递增 1。

updateCountHandler 被传递给附加到按钮的 onClick 事件。

每次单击按钮时，updateCountHandler 都会调用“setCount”来将计数加 1。

“使用状态”提供的“计数”状态变量将反映更新后的值。

如果想要显示“计数”值，可以使用 JSX 中的 useState 函数提供的“计数”。

**React 状态更新成批发生。**

这意味着您可能不会像预期的那样很快看到更新的状态值。

再举一个例子来理解吧。

假设我们的按钮现在在点击时执行一些异步操作，我们需要计算同一个按钮的点击次数。

为了模拟异步特性，我们可以添加 2 秒的超时。

基于我们到目前为止对 useState hook 的理解，我们可能会提出如下解决方案:

```
import "./styles.css";
import { useState } from "react";export default function App() {
  const [count, setCount] = useState(0);
  const updateCountHandler = () => {
    setTimeout(() => {
      setCount(count + 1);
    }, 2000);
  };
  return (
    <div className="container">
      <button onClick={updateCountHandler}>Click</button>
      <p>No. of clicks: {count}</p>
    </div>
  );
}
```

根据上面的代码片段，您可能会期望“计数”的值与点击次数保持同步。

但这并没有发生。

它不能像预期的那样工作，因为 React 的状态更新不是瞬时的，而是成批的。在“计数”中反映当前状态值需要时间。

因为“计数”没有最新的状态值，所以我们将“计数”的旧值增加 1。

React 为我们提供了另一种 useState 钩子的变体来避免这种情况。

下面让我们来看看它的实际应用。

```
import "./styles.css";
import { useState } from "react";export default function App() {
  const [count, setCount] = useState(0);
  const updateCountHandler = () => {
    setTimeout(() => {
      setCount((prevCount) => prevCount + 1);
    }, 2000);
  };
  return (
    <div className="container">
      <button onClick={updateCountHandler}>Click</button>
      <p>No. of clicks: {count}</p>
    </div>
  );
}
```

下面的代码片段让一切变得不同:

```
setCount((prevCount) => prevCount + 1);
```

我们将一个箭头函数传递给这个“setCount”更新函数的变体。React 在这里插入前一个状态值，不管它是否反映在“计数”状态变量中。

“prevCount”可以是任何名称。唯一要记住的是，函数传递给状态更新函数的第一个参数将总是前一个状态值。

## 外卖食品

useState 是 React 中最常用的钩子之一，因此也是最重要的一个。

我希望这篇关于 useState 的文章已经让您对 React 中的钩子工作有了一个很好的基本了解。

如果你想了解更多，我推荐你看看下面的参考资料。

在那之前，

编码快乐！

## 参考资料:

*   [钩子 API 引用](https://reactjs.org/docs/hooks-reference.html#usestate)
*   [使用状态挂钩](https://reactjs.org/docs/hooks-state.html)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**