# React 官方回答:React18 中请求数据的正确方式(其他框架也适用)

> 原文：<https://javascript.plainenglish.io/react-official-answer-the-right-way-of-requesting-data-in-react18-other-frameworks-also-apply-50d907c1f6c4?source=collection_archive---------3----------------------->

## React 18 中使用 useEffect 进行数据提取有哪些问题？

![](img/7ac577546ac5b689083eb19d7ba7c794.png)

Photo by [Jonatan Pie](https://unsplash.com/@r3dmax?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有些学生喜欢以下列方式用 useEffect 请求初始数据:

```
useEffect(() => {
  fetch(xxx).then(data => setState(data.json()))
}, [])
```

但是 React18 并不推荐这种方式。这样写有什么问题？如果这个不推荐，推荐的方式是什么？[让我们来看看 Dan 是如何回应上面 Reddit 的问题](https://www.reddit.com/r/reactjs/comments/vi6q6f/what_is_the_recommended_way_to_load_data_for/)的。

## 这是一个常见的问题。

除了 React，大多数组织为“组件”的前端框架都有类似的 API，如下所示:

*   影响
*   didMount/didUpdate

如果需要“初始化时请求数据”，这类框架选择在上述回调函数内执行请求操作，并在数据返回时更新状态。所以，这不是一个需要反应的独特问题。相反，他很普通。

它在 React 中如此突出的原因是 React 官员正在引导开发人员远离以这种形式编写代码(通过说“useEffect 在严格模式下执行两次”来放大问题)。React 这样做的原因是为了项目的“性能”和“UX”(用户体验)。我们再来谈谈这其中的含义。请注意，这些含义也适用于其他框架。为什么不推荐这个？

## **比赛条件**

在 useEffect 中请求数据时，您面临的第一个问题是“需要解决竞争条件问题”。假设您有一个组件用户，它接收 userID 作为道具，并在用 userID 请求数据后显示用户信息。你应该这样写:

这里有一个在开发阶段很难重现的 bug 如果 userID 变化得足够快，就会发起多个不同的用户请求。最终显示哪个用户的数据，取决于先返回哪个请求。这就是“请求竞争问题”。

## 单击后退按钮后重新请求数据

如果用户导航到一个新页面，然后通过浏览器的后退按钮返回到当前页面，他不会立即看到跳转之前所在的页面。相反，他可能会看到一个白屏——因为他仍然需要重新执行 useEffect 来获取初始数据。这个问题的本质原因是没有缓存初始数据。

## 在 CSR 期间，白屏时间

当在 CSR(客户端呈现)期间请求 useEffect 中的数据时，页面是白色的，直到数据被返回。

## 瀑布问题

如果父组件和子组件都依赖 useEffect 进行初始数据呈现，那么整个呈现流程如下。

1.  父组件安装
2.  父组件 useEffect 执行并请求数据
3.  返回数据后，将重新呈现父组件
4.  子组件安装
5.  子组件 useEffect 执行并请求数据
6.  返回数据后，将重新呈现子组件。

如您所见，当父组件的数据请求成功时，子组件甚至还没有开始呈现第一个屏幕。这就是渲染中的瀑布问题——数据像瀑布一样往下流，到达的组件才开始渲染，效率很低。

![](img/a74120c719dedb137486068b38cd88a8.png)

Photo by [Mike Lewis HeadSmart Media](https://unsplash.com/@mikeanywhere?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

既然直接写 useEffect 有这么多问题，有什么推荐的方式？

## 推荐的方式

在 Meta 中，数据是基于中继驱动的(但是请求数据需要 GraphQL)，所以很难在社区中推广这种架构。然而，社区现在有了一个成熟的“请求数据的解决方案”

*   SSR，可以用 Next.js 和 Remix 来接管数据请求。
*   CSR，您可以使用 React Query 和 useSWR 来接管数据请求。

所有这些成熟的解决方案都致力于解决上述问题。如果不想用这些解决方案，想自己写，可以参考新 React 文档中的以下两篇文章。

[使用效果同步数据](https://beta.reactjs.org/learn/synchronizing-with-effects#fetching-data)

[你可能不需要特效](https://beta.reactjs.org/learn/you-might-not-need-an-effect#fetching-data)

可以看看我写的总结——[新 React 文档:不要滥用效果](/the-new-react-document-dont-abuse-effect-2ee10a6b4718?source=your_stories_page-------------------------------------)

[](/the-new-react-document-dont-abuse-effect-2ee10a6b4718) [## 新 React 文档:不要滥用效果

### 当您或您的同事使用 useEffect 挂钩时，是否出现过以下情况？

javascript.plainenglish.io](/the-new-react-document-dont-abuse-effect-2ee10a6b4718) 

## 摘要

在本文中，我们讨论了请求数据的“**不推荐方式”和 React18 后请求数据**的“**推荐方式”。“不推荐的请求数据的方式”不仅仅存在于 React 中，很多前端框架都有这样的问题。**

***欢迎关注我关于***[***Twitter***](https://twitter.com/yanghui0324)*[***LinkedIn***](https://www.linkedin.com/in/hui-yang-075076245/)***，以及***[***GitHub***](https://github.com/guchen-yh)***！****

*写作一直是我的激情所在，它带给我帮助和激励他人的快乐。如果您有任何问题，请随时联系我们！*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。**