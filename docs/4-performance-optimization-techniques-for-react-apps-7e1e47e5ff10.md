# React 应用的 4 种性能优化技术

> 原文：<https://javascript.plainenglish.io/4-performance-optimization-techniques-for-react-apps-7e1e47e5ff10?source=collection_archive---------5----------------------->

## 还有很多其他方法可以优化 React 应用程序。不是所有的都适用于每一个应用程序，也不是你做的每一件事都能显著提高性能。

![](img/56f6fbf562f5299685483ffe87d0fcbf.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我最近被分配了一个任务，上面写着“提高应用程序的性能”。这是我记录的旅程。

## 步骤 1 —找到性能开始下降后的场景

幸运的是，当性能下降到用户体验绝对无法忍受的程度时，我被告知这种情况。为了找出所有这样的场景，人们需要严格地在应用程序上执行各种操作，并在性能开始下降时保持监控。没有直接的方法可以做到这一点，唯一的方法是让越来越多的人使用该应用程序并报告他们的经历。另一种方法也可以是生成大量虚拟数据，并尝试将其全部加载到 UI 上，然后观察它的表现。此外，不要期望一次找到所有的场景，您会不断地发现它们，然后您可以执行下面的步骤来提高每个场景的性能。

## 步骤 2 —调试并尝试找到真正的问题所在

下一步是调试，看看是什么真正导致了性能的滞后或下降。为此，您可以使用开发工具中的 profiler，也有一种方法可以突出显示在特定操作中重新呈现的所有组件。对我来说，这两个工作得最好，因为它们帮助我理解什么被重新渲染，分析器也告诉我为什么。分析器还会告诉你哪些组件花费了多少时间进行渲染，以及你的应用程序总共需要多少周期才能达到就绪状态。此外，如果我看到嵌套循环，我还会使用 javascript 中的 *console.time()* 方法，看看这些循环是否需要很长时间才能完成。在我的场景中，我得到了一些正面的见解，即我们使用的 React 上下文导致了主要问题。

[点击这里阅读关于 React Profiler 的所有信息](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html)。

## 步骤 3 —使用以下技术来提高性能

我将在这一部分列出我所做的帮助我提高应用程序性能的事情。

1.  ***从状态中移除真正不需要重新渲染组件的变量:*** 我们有两个上下文，总共有大约 10-15 个状态变量。这样做的问题是，每次由于 setState 而重新呈现上下文时，它都会继续并导致所有使用该上下文的子节点重新呈现。我删除了所有没有理由继续并重新呈现组件的状态变量，还删除了所有作为值传递给上下文提供者的变量，这些变量可能是派生的，或者没有在应用程序中的任何地方使用。这是很重要的学习，我们倾向于把一切放在上下文中，而你应该只添加你真正需要的。
2.  ***在正确的地方使用了上下文:*** 我在一些组件中看到我们调用了上下文，但是没有真正使用上下文的任何属性。相反，我们将它作为道具传递给子组件。这导致了大量的重新渲染，因为上下文中的重新渲染将触发组件 A 重新渲染，这将导致组件 B、C 和 D 及其所有子组件重新渲染。上下文只在组件 D 中需要，所以我直接将上下文移到了子组件中。我在每个看到上下文变量作为道具传递给子组件的地方都这样做。
3.  **这种方法没有错，但是如果子组件调用了几个 useEffects 或者正在调用其他 API，那么将被 null/empty 检查的数据移动到父组件是有意义的。您根本不需要将子组件呈现给 DOM，因为它没有任何值。这将保存应用程序渲染子对象可能带来的所有性能损失，并调用其中的所有钩子和 API。**
4.  ***重构代码:*** 我执行的一个常规步骤是试图理解编写的代码，尤其是数据被操作、添加到数组、或者我们使用了嵌套循环等等的地方。在有意义的地方将数组转换为映射，进一步从 useEffect 依赖数组中移除变量，在那里它们不添加任何值，最后还移除了对没有意义的数据的检查。对于不同的应用程序，这一步可能是不同的，必须非常小心地完成，因为你不希望破坏已经在工作的东西。所以理想情况下，试着尽可能深入地研究，首先理解逻辑，然后如果你有信心，继续重构它。

![](img/ff4e2bb196093622da704373cfbf674d.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/charts?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 结论—

使用上述方法，我能够为我的应用程序减少大约 25-30 次重新渲染。在性能受到严重影响的情况下，初始页面加载时间缩短了几秒，响应时间也缩短了一两秒。这是一段旅程，我仍在努力让:D 变得更好

最后，还有很多其他方法可以优化 React 应用程序。不是所有的都适用于每一个应用程序，也不是你做的每一件事都能显著提高性能。有时问题很明显，解决它们会使应用程序具有很高的性能，而在其他情况下，问题很复杂，很难提高性能。但总的来说，优化你的代码是一个有趣的旅程，你会学到很多东西，大多数时候，你会学到一个诀窍，你会觉得为什么我不早点知道呢？

经常花时间重构你的代码，经常花时间评估性能，因为如果你不这样做，它可能会突然变得太晚。

感谢你花时间阅读这篇文章，如果你想和我聊聊天或者对我的文章有什么建议，请在下面留言。你也可以通过 [Telegram](https://t.me/iambhavyamehta) 、 [LinkedIn](https://www.linkedin.com/in/bhavya-y-mehta/) 或 [Instagram](https://www.instagram.com/iambhavyamehta/) 联系我。

最后，如果你希望我继续写作并支持我，你可以在这里给我买杯咖啡。[支持 Bhavya](https://super.page/bhavya) 。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****