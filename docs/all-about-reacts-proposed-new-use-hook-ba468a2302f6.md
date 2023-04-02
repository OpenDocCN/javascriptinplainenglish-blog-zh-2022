# 关于 React 提出的新用途()钩子的所有内容

> 原文：<https://javascript.plainenglish.io/all-about-reacts-proposed-new-use-hook-ba468a2302f6?source=collection_archive---------0----------------------->

## 对承诺的一流支持开始起作用了——这是关于它应该如何运作的建议

来自 React 核心团队的[功能提案在 React 生态系统中引起了一些反响，既吸引了对其新功能的兴奋，也引起了对其将如何实现的一些关注。在这篇文章中，我们将深入探讨这个新特性看起来像什么，它解决了什么问题，以及提出了什么问题。](https://github.com/acdlite/rfcs/blob/first-class-promises/text/0000-first-class-support-for-promises.md#example-use-in-client-components-and-hooks)

![](img/98e26b26432b94a9a3646aa08694f28d.png)

Hooks, of the non-React variety. Photo by [Anne Nygård](https://unsplash.com/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# RFC:对承诺的一流支持

这个新特性完全是为了在 React 中获得对承诺的“一流”支持，并在 React 核心贡献者的 RFC(征求意见稿)中进行了描述:

[](https://github.com/acdlite/rfcs/blob/first-class-promises/text/0000-first-class-support-for-promises.md#example-use-in-client-components-and-hooks) [## rfcs/0000-一级支持承诺. md at 一级承诺 acdlite/rfcs

### RFC 对变更做出反应。在 GitHub 上创建一个帐户，为 acdlite/rfcs 的发展做出贡献。

github.com](https://github.com/acdlite/rfcs/blob/first-class-promises/text/0000-first-class-support-for-promises.md#example-use-in-client-components-and-hooks) 

该文档名为“对承诺的一流支持，async/await ”,描述了将使用承诺的代码更好地集成到 React 组件中的新特性。

RFC 并不一定意味着某个特性将被实现——任何人都可以编写一个 RFC 并在 React RFCs repo 中打开一个 pull 请求。不过，在这种情况下，来自 React 核心贡献者并得到高级别的支持，RFC 似乎有可能以这样或那样的形式被接受，并且该特性会在 React 的未来版本中找到自己的路。

# 这解决了什么问题？

如果您正在使用执行任何类型的服务器通信或其他异步计算的 React 组件，那么您当前需要使用 Promises 或其他类型的回调模式自己处理该行为。下面是一个典型的代码片段，用于发出服务器请求并在组件内部呈现结果:

```
const WidgetList = () => {
  const [widgets, setWidgets] = React.useState([]) React.useEffect(() => {
    widgetsAPI.get().then((r) => {
      setWidgets(r)
    })
  }, []) return (<div>
    {widgets.map(w => (<p id={w.id}>{w.name}</p>))}
  </div>)
}
```

在这个例子中，我们的`widgetsAPI`调用返回一个承诺。然后我们得到调用的结果，并通过`then`回调来设置组件状态。这是一种常见的模式，它工作得相当好——但是也相当冗长，并且随着组件的增长会使组件变得复杂。

从表面上看，在组件中支持承诺的最直接方式是使用 JavaScript 现有的 async/await 功能:简单地`await`承诺并使用结果！

```
const widgets = await widgetsAPI.get()
```

事实上，服务器渲染的 React 组件*将*支持异步渲染，从而可以`await` 承诺的结果完全如上图所示。

但是客户端呢？在浏览器中，React 组件暂时不能被设为异步。正如现在经典的[你的函数是什么颜色](https://journal.stuffwithstuff.com/2015/02/01/what-color-is-your-function/)中所描述的，我们不能在非异步函数内部调用`await`。RFC 讨论了这一限制以及支持异步客户端组件的未来计划:

> 我们强烈认为不仅要支持异步服务器组件，还要支持异步客户端组件。这在技术上是可能的，但是有足够多的陷阱和警告，到目前为止，我们还不习惯将这种模式作为一般的建议。计划是在运行时实现对异步客户端组件的支持，但是在开发期间记录一个警告。文件也将阻止它们的使用。

所以现在还没有异步客户端组件——但是这又会给我们带来什么呢？我们如何在客户端实现一流的承诺支持？

解决方案是一种新的名字很好听的钩子。

# 解决方案:新的 React 使用()钩子

客户端异步问题的解决方案是一个新的钩子，简单地命名为`use()`。钩子的功能在实践中非常类似于`await`，但是有一些重要的区别:

```
const WidgetList = () => {
  const widgets = use(widgetsAPI.get()) return (<div>
    {widgets.map(w => (<p id={w.id}>{w.name}</p>))}
  </div>)
}
```

就像`await`一样，使用有效解封我们`widgetsAPI`返回的承诺值。然而，与`await`不同的是，当承诺被解决时，组件的执行实际上并不从相同的地方恢复。相反，`use`抛出异常，就像`React.Suspense`中断渲染一样。当承诺解决时，组件被*重新呈现:*

> 当承诺最终解决时，React 将*重放*组件的渲染。在随后的尝试中，`use`调用将返回承诺的履行值。

这两种方法的最终结果*应该是*相同的，但是在行为上有潜在的差异。回想一下，`await`只是调用`promise.then(callback)`的语法糖。所以当 promise 用`await`解决时，执行从完全相同的位置重新开始。但是当 promise 用`use`解析时，部分组件代码被*重新运行*并且`use`调用将返回结果值。

现在这个*不应该*有所不同，因为如 RFC 所述，React 组件应该是等幂的:用相同的道具、状态和上下文重新渲染不应该改变结果:

> 重放依赖于 React 组件需要是等幂的属性——它们在渲染期间不包含外部副作用，并且对于给定的一组输入(道具、状态和上下文)返回相同的输出。

然而，在实践中，即使非幂等行为是错误的，也肯定有可能以触发副作用的方式构建一个组件，最终导致执行两次。举一个简单(无害)的例子，假设您的小部件 API 函数中有一个`console.log`。使用`async`实现，您会看到控制台记录了一个值。随着`use`的实现，你会看到两个。

此外，`use`钩子的“第二次执行”引入了另一个约束:API 调用*必须*缓存结果，以便在第二次调用发生时它们(或多或少)立即可用:

> 只有当数据请求被缓存时，在挂起之前等待微任务刷新的机制才起作用。更准确地说，约束是:在没有接收新输入的情况下重新呈现的异步函数必须在微任务内解析。

如果您的 API 不支持缓存(或者没有正确实现缓存)，而是返回了另一个在微任务中无法解析的承诺(例如，它启动了一个新的 API 调用)，React 将再次挂起组件呈现—大概会导致一个继续进行 API 调用并且永远不会完成的循环！明确地说，这种情况可能是开发人员的错误，但也可能是容易犯的错误。

有趣的是，与其他 React 钩子不同，`use`钩子不受钩子的[规则的约束，这意味着它可以在循环中被有条件地调用。这种怪癖在某种程度上是由缓存需求造成的:第二次呈现可以调用 use with a "new" promise，它访问相同的数据并应该得到缓存的结果。没有必要跟踪`use`钩子调用的顺序，这就是为什么其他钩子*遵循那些规则。*](https://reactjs.org/docs/hooks-rules.html)

# 这种方法有哪些问题？

虽然在 React 中获得对承诺的一流支持是令人兴奋的，但我个人有许多担忧——根据讨论，许多担忧也是其他人共有的。我不会假装对所有这些问题都有正确的答案，但这里有一些我在讨论中关注的问题。

## 名字

当然，命名这是计算机科学中最困难的问题，但是名称`use()`非常普通，并没有真正表达这个函数做什么以及它如何与承诺一起工作。

RFC 确实解决了这个问题，并指出`use()`有望在未来与其他类型的“解包”一起工作，也许是与上下文或其他数据类型一起工作。此外，他们指出`use()`的名字清楚地表明它是一个“只反应”的函数。这些都是合理的解释，但它们确实导致了下一个问题，这是围绕着`use()`的特定行为怪癖。

## 使用()与其他挂钩的不同规则

如前所述，`use()`被免除了正常的钩子规则。这是，同时，精彩和困惑。

它很棒，因为它消除了我们使用它的一些限制。

但是它*混淆*是因为——如果它不遵循钩子的[规则，那它实际上是钩子吗？这又让我们回到了之前的问题:`use()`真的是正确的名字吗？](https://reactjs.org/docs/hooks-rules.html)

我担心的是`use()`和其他钩子之间的规则差异会让新开发者更难理解钩子的规则，事实上，更难理解钩子的核心是什么。

## 对 use()调用的代码的新约束

虽然新的 use()钩子不像其他钩子那样受到相同的约束，但它确实在使用的代码周围引入了新的行为约束。也就是说，关于缓存的需求和产生传递给`use()`的承诺的代码副作用的缺乏。

虽然缓存行为肯定是一个合理的需求，但它并不是由任何接口或契约强制的。它基于从调用 API 函数的地方的*隐含知识，对 API 函数的开发者施加约束。*

与其将这一负担推给开发人员，也许缓存需求可以通过 API 变更和依赖数组(如`useEffect`)在内部处理:

`use(() => myAPI.fetch(id), [id])`

注意，这种方法的实现可能会使 use()钩子也遵循“正常的”钩子规则(以便“记住”正在使用哪个调用)。这不一定是坏事！

## 不同的客户机/服务器组件行为

随着`use()`在客户端的引入和`await`在服务器端的引入，客户端和服务器组件的代码、生命周期和行为(以及它们接触的代码)开始以微妙但有意义的方式产生差异。这阻碍了代码重用和代码理解。

我不同意 RFC 中的观点:

> 尽管我们最初有些犹豫，但是在服务器和客户机上使用不同的方法访问数据也有一个好处:这使得跟踪他们在哪个环境中工作变得更加容易。
> 
> 服务器组件应该和客户端组件感觉相似，但是我们不希望它们感觉*太*相似。每个环境都有不同的功能，开发人员在构建应用程序时需要清楚这种区别。

如果有人在跟踪他们所处的环境方面有困难，我怀疑函数定义中的 *async* 关键字是否能达到目的。

如果真正的目的是跟踪不同的环境并验证行为，那么有很多更好的方法来明确地做到这一点，例如，为客户端服务器模块或 API 使用不同的名称空间，引入一个 T2 包装器，等等。上面的解释听起来像是对不同 API 的事后证明。

# 承诺，承诺…

我认为在 React 中获得对承诺的一流支持是一个好主意，但我并不完全赞同提议的解决方案。幸运的是，这仍处于提议阶段，在[拉动请求](https://github.com/reactjs/rfcs/pull/229)中有许多关于它的良好对话，包括围绕本文提出的问题的讨论等等。

就个人而言，考虑到这种方法的一些问题，我认为等待异步客户端组件得到解决并不是最糟糕的策略:与其发明一个新的、棘手的、只反应的东西，不如花时间让它与 JS 开发人员处理问题的标准方式`async/await`一起工作。与此同时，在回调中解开值并不是世界末日。

但是我愿意相信也许我错了，如果这对于 React 开发人员来说是一个主要的生产力优势，那么现在的改变是值得的。你对提议的新`use()`挂钩和一级承诺支持有什么想法？

最初发布于 [Blixtdev](https://blixtdev.com) 。

乔纳森写了一些关于创业、软件工程和健康科学的文章。如果你喜欢这篇文章，请考虑加入 Medium 来支持 [*Jonathan 和其他数千位作者*](https://medium.com/@jonnystartup/membership) *。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)***