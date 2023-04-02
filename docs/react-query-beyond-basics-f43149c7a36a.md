# React 查询:超越基础

> 原文：<https://javascript.plainenglish.io/react-query-beyond-basics-f43149c7a36a?source=collection_archive---------6----------------------->

![](img/d6e956ca75aa8c78184a76d8c9cae219.png)

Photo by [Benjamin Voros](https://unsplash.com/@vorosbenisop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/mountain-night-sky?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

互联网上的各种文章已经讨论了使用 react-query 的好处。`useQuery` / `useMutation`的易用性，即基本上是一行代码，用来访问加载、获取或错误状态以及响应数据，已经被反复迭代了。但更高级、更小众的功能几乎没有讨论过。所以我在这里，深入研究了 react-query 世界的一些特性。

我将给你一个简单的待办事项列表应用程序的例子，其中显示了待办事项列表。当用户想要创建新的 todo 时，会打开一个模态表单。成功创建待办事项后，将重新提取待办事项列表。在待办事项列表中，如果用户点击一个待办事项，它将转到一个新的页面，该页面将显示与该待办事项对应的详细信息。

# **1。onSucces & onError**

`useQuery`和`useMutation`都支持各种配置选项。其中两个是接受函数的`onSuccess`和`onError`参数。这两个选项很有帮助，尤其是当我们想要执行一些非数据呈现逻辑时。在 todo 列表的例子中，如果我们想抛出一个成功或错误的消息芯片，不一定是一个组件，use 可以使用这些。(*如果需要渲染组件，我们最好用* `*isSuccess*` *或者* `*isError*`)。基本上，这可以像我们在 api 获取中使用的`.then`中的回调函数一样。更好的用例是分派一些 redux 状态。这也可以在这里完成，不需要到处摸索。

# 2.查询无效

在我们的待办事项列表示例中，正如我们已经讨论过的，我们希望在成功创建任务时重新获取所有待办事项的列表。所以查询失效的魔力来了。我们必须使用前面讨论过的`onSuccess`函数。在该函数中，我们可以使用 queryClient invalidation 来使无效，即要求 react-query 重新提取一个或多个查询。

在我们的 todo 应用程序中，当我们的 create todo 成功时，我们将使获取所有 todo 列表的查询无效。

# 3.查询重试次数

这可能很小，但在情况需要时可以派上用场。React query 带有一些对应于每个配置选项的预配置默认值。例如，缓存时间为 5 分钟，过时时间为 0。所以众多选项中的一个，就是`retry`选项。其默认值为 3。也就是说，如果一个查询在第一次尝试中获取查询不成功，它将继续尝试 3 次，然后将`isError`声明为真。在某些情况下，你可能不希望这种行为。您可以随时将其更改为其他数字，表示您希望发生的重试次数。另一种方式是，retry 也接受 true 和 false 作为值。那是什么意思？如果 retry 为 true，那么 react query 将获取查询，直到成功；如果 retry 为 false，那么在任何不成功的尝试之后都不会重试。

所有这些选项都可以根据每个查询进行更改。但是您可能希望为所有查询声明自己的配置选项(除非您在某个特定查询中另外指定)。那么您应该考虑在查询客户机中这样做。

# 4.有条件地启用查询

在某些情况下，您可能希望查询仅在满足某些条件时运行。`useQuery`react-query 的所有其他优点都是钩子，不能直接用在 if-else 语句中，因为那会破坏 react 钩子的基本规则。对于这些类型的场景，react-query 带有一个名为`enabled`的选项。我们总是可以将它们硬编码为真或假，但是真正精彩的地方是当一个变量被传递时。现在，根据变量值的变化，查询将被启用或禁用。多酷啊！

例如，在我们的 todo-list 应用程序中，当用户转到单个 todo 时，`todo_id`作为 url 中的参数传递(使用 react-router 或其他路由库)。并按`todo_id`，取明细。现在，我们希望获取查询，前提是 param 不为空。我们可以这样做-

# 5.查询的自定义挂钩

这更多的是个人观点，而不是 react-query 特有的特性。因此，如果您需要定制预配置选项之外的行为，或者需要访问`onSuccess`或`onError`选项，很快您可能会得到类似这样的结果。有些人可能更希望可以立即看到查询中发生了什么。但是，如果您需要跨多个组件访问同一个查询，您可能希望在整个 react-query 逻辑周围创建自己的定制钩子。我向你保证，这不是什么高端柔术。如果我们考虑前面的例子，它会是这样的:

> 一些专业建议

1.  如果你考虑编写自定义钩子，你也可以考虑声明一个变量，在这里我们只是保存数据，或者如果你出于某种原因需要状态代码，那么你也可以在这里把它抽象出来，作为单个值传递，并生成我们需要映射或执行其他操作的数据。定义良好的变量比一般数据更有意义。

2.如果将数据重命名为其他名称，也可以直接在 react-query 中完成。不仅仅是数据，你还可以将`isLoading`或`isError`重命名为其他名称。如果您需要在一个组件中访问两个或多个查询，这是非常必要的。

3.您可以使用 api 路由作为查询名称。如果将您的查询函数抽象到其他地方，这将非常有意义。如果您发现您需要访问您认为已经在某些组件中使用过的特定查询，这可能也会有所帮助。现在你想在其他组件中使用它。以这种方式命名，您将很容易避免查找特定查询的名称。毕竟，查询名称对于有效利用 react-query 的优势(例如，查询无效)是至关重要的。我在整篇文章中都遵循了这种风格。

4.如果使用定制钩子，你可以考虑根据它们的主要路径将它们保存在单独的文件中。并将它们都保存在服务文件夹本身中，这种结构可能已经在 axios 中使用了。

```
src
 — components
 — pages
 — services
  — todo.js
  — user.js
```

它并不意味着详尽无遗。就几个，我每天都在用。

最后的一些部分是纯粹的个人黑客，你可能不同意，或者我可能真的做错了。请随时告诉我。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***