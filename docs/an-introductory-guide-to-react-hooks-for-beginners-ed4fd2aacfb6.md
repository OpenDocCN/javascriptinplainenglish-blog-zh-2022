# 初学者使用 React 钩子的入门指南

> 原文：<https://javascript.plainenglish.io/an-introductory-guide-to-react-hooks-for-beginners-ed4fd2aacfb6?source=collection_archive---------9----------------------->

## React 钩子的简单介绍以及为什么你应该关心它们。

![](img/a6cf3a47298c75363bbdfea5d63b2066.png)

Photo by [Trophy Technology](https://unsplash.com/es/@trophytechnology?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 16.8 推出的时候，hooks 作为一个新的附加物加入其中。这是 React 16.8 中包含的稳定版本，由 Sophie Alpert 和 Dan Abramov 在 React 16.8 年大会上发布。

这个版本是第一个支持钩子的稳定版本。什么是钩子？基本上，钩子允许你使用 React 特性和状态，而不需要写类。类没有被根除，但是钩子确保你不再需要依赖类来使用 React 的特性。

现在让我们深入了解钩子以及它们是如何使用的。

## 为什么用“钩子”这个词？

钩子允许你*钩子*进入 React 的状态和特性，而不用为它写任何类。

大多数开发人员发现，职业对他们来说是非常混乱的，当学习 React 时，这对一些人来说是一个巨大的挫折。无论您想要重用特定的代码还是有效地组织它，类就像是这两者之间的一堵墙，导致了很多混乱。

班级制造了更多的问题。为了确保类不会影响 React 的流行，引入了钩子。

所以，是的！钩子允许你使用 React 状态和特性，不需要任何类的帮助，你也不需要在 React 上写类。

## 内置挂钩

目前 React 使用了一些内置的钩子比如`useState`和`useEffect`。让我们用例子来看看这两者。

## 使用状态示例

`useState`用于更新状态，并在更新/重新渲染后保留状态值。

让我们看看官方 React [文档](https://reactjs.org/docs/hooks-state.html)中提供的例子，因为这是一个相对简单的例子。

```
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"  
const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

如文档中所述，`useState`是*“一个让你给函数组件添加反应状态的钩子。”*

我们在这里所做的基本上是使用`count`作为一个状态变量，并在我们每次点击“点击我”按钮时更新它的值。

让我们分解下面的语句来理解语法是如何工作的。

```
const [count, setCount] = useState(0);
```

我们在这里所做的是声明一个“状态变量”——在本例中是`count`。它不需要这么叫——事实上它可以叫任何名字。此外，与类组件不同，状态不必是对象；例如，`count`这里是一个数字，但是如果需要的话，我们也可以使用字符串。在这个特殊的例子中，我们试图在每次用户点击“Click me”按钮时更新 count 变量。

`useState(0)`表示`count`的初始值为 0。传递给 useState 钩子的参数总是状态变量的初始状态。在这种情况下，它将意味着第一次单击“单击我”按钮会将`count`的值设置为 1，在重新渲染后会被 React 保留，第二次我们单击它时，它将被设置为 2，以此类推。这是因为，与普通变量不同，状态变量由 React 保存。

现在让我们进入`setCount`。同样，根据文档，*“*`*useState*`*钩子总是返回一对值:当前状态和更新它的函数。”*当我们点击“Click me”按钮时，调用`setCount`函数，在这种情况下，我们传递参数`count + 1`，导致状态变量`count`增加 1，该值将在我们点击按钮后由状态更新引起的重新呈现后保留。

这就是我们如何使用`useState`钩子更新状态。

## 使用效果示例

`useEffect`是另一个内置挂钩。您知道，日期获取和订阅可以被称为 React 中的副作用，因为它们会影响其他组件。

因此，`useEffect`是您可以使用功能组件来执行效果的东西。根据[文档](https://reactjs.org/docs/hooks-effect.html)、*，“获取数据、设置订阅以及手动更改 React 组件中的 DOM 都是副作用的例子。”*

同样，为了简单起见，让我们以 React [文档](https://reactjs.org/docs/hooks-effect.html)中的例子为例，它使用了与我们在上面看到的`useState`中相同的反例。

```
import React, { useState, useEffect } from 'react';
function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:  useEffect(() => {    // Update the document title using the browser API    
document.title = `You clicked ${count} times`;  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

让我们明白这是怎么回事。

> **注意:**如果你熟悉类组件，那么你可以把`useEffect`钩子想象成`componentDidMount`、`componentDidUpdate`和`componentWillUnmount`的组合。

默认情况下，`useEffect`钩子在每次渲染后运行，包括第一次初始渲染和每次更新后。React 更新 DOM 后，有时会运行一些额外的代码。例如，发出网络请求(从 API 获取数据)或记录日志。

在最基本的层面上，`useEffect`钩子告诉 React 在渲染之后你的组件需要做一些事情。我们通常将一个函数作为参数传递给`useEffect`。React 会记住这个函数，在 DOM 更新完成后，React 会调用它。

为了简单起见，这里的文档显示了设置文档标题(所以在这个例子中，在你点击按钮并更新状态之后，有一个重新呈现，post-函数被调用，标题被设置)但是我们也可以使用它从前面提到的 API 获取数据。

我保持事情简单，因为这是一篇介绍性文章，但你可以玩它，并得到它的窍门。

## 使用挂钩的规则

根据钩子的官方文档，基本上有两个必须遵守的主要规则。

第一条规则是你不应该在任何函数和循环中调用钩子，因此钩子只能在顶层调用。

第二条规则简单的说明了你应该只从 *React 函数组件*中调用钩子，避免使用其他包含的函数来调用它。

在 React 中使用钩子时，你必须记住这两条简单的规则。

我希望这个关于什么是钩子的简单介绍对你有用。目前，在使用 React 的各种 JavaScript 开发人员中，挂钩是一种趋势。基本上，钩子因为其易用性和高效性而越来越受欢迎。坚持编程，坚持练习。祝你的编程之旅好运！

[***用我的推荐链接给自己买一个 5 美元的中级会员，点击这里(我得到一小笔佣金，它直接支持我，不需要你额外付费)***](https://aniketz.medium.com/membership)

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 阅读 Aniket 上的每一个故事(以及媒体上成千上万的其他作者)。你的会员费直接支持了一个市场…

aniketz.medium.com](https://aniketz.medium.com/membership) 

[***想加入我的简讯了解更多此类内容，请点击这里***](https://aniketz.medium.com/subscribe)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*