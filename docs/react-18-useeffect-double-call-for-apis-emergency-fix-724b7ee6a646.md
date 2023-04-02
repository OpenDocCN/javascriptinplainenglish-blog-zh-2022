# 对 API 的双重调用:紧急修复

> 原文：<https://javascript.plainenglish.io/react-18-useeffect-double-call-for-apis-emergency-fix-724b7ee6a646?source=collection_archive---------0----------------------->

![](img/49a044d255995d5275682e3206bc04be.png)

React 18 API Calls need an Emergency Fix!

所以你已经升级到 React 18，启用了[严格模式](https://reactjs.org/docs/strict-mode.html)，现在你所有的使用效果都被调用了两次。

这通常是好的，但是你在你的 useEffects 中有 API 调用，所以你在开发模式中看到双重流量。听起来熟悉吗？没问题，我会帮你解决一些潜在的问题。

# 解决方法 1:接受现实

一个合理的选择就是忍受它，这只是开发模式的行为。它还试图通过对您的组件进行压力测试来帮助您，以确保它们与 React 中的未来功能兼容。但是，嘿，我明白，你在这里，你不喜欢它，所以…让我们继续前进。

# 修复 2:删除严格模式

是严格模式导致了双重渲染，所以另一个选择就是删除它。在`index.js`中使用了现成的 StrictMode 组件，它在这里:

```
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

简单地把它拿掉，就像这样:

```
root.render(<App />);
```

也就是说，我不推荐这种方式，因为严格模式对你的应用程序代码做了很多有益的检查，所以你真的要考虑保留它。

# 修复 3:使用中止控制器

另一个修复方法是使用 AbortController 来终止来自第一个`useEffect`的请求。假设这是您的代码:

```
 const [people, setPeople] = useState([]);
  useEffect(() => {
    fetch("/people")
      .then((res) => res.json())
      .then(setPeople);
  }, []);
```

这段代码在 React 17 中没什么问题，但在 18 中的严格模式下，在开发模式下挂载、卸载和重新挂载组件会出现问题。这表明，如果在卸载组件之前没有完成获取，您不会中止获取。所以让我们补充一下`AbortController`的逻辑。

```
 useEffect(() => {
 **const controller = new AbortController();**    fetch("/people", **{
      signal: controller.signal,
    }**)
      .then((res) => res.json())
      .then(setPeople);
 **return () => controller.abort();**  }, []);
```

代码非常简单。我们创建一个新的`AbortController`，然后将它的`signal`传递给`fetch`，在我们的清理函数中，我们调用了`abort`方法。

现在将要发生的是，第一个请求将被中止，但第二个装载不会中止，提取将成功完成。

我认为大多数人会使用这种方法，如果不是因为一件事，在 Inspector 中你会看到两个请求，其中第一个是红色的，因为它已经被取消了，这很难看。

# 修复 4:创建自定义提取器

JavaScript 承诺的一个很酷的方面是，您可以像使用缓存一样使用它。一旦承诺被解决(或拒绝),您可以继续调用`then`或`catch`,您将获得解决(或拒绝)的值。它不会**而不是**对已实现的承诺发出后续请求，它只会返回已实现的结果。

由于这种行为，您可以构建一个创建自定义缓存`fetch`函数的函数，如下所示:

```
const createFetch = () => {
 *// Create a cache of fetches by URL*  const fetchMap = {}; return (url, options) => {
 *// Check to see if its not in the cache otherwise fetch it*    if (!fetchMap[url]) {
      fetchMap[url] = fetch(url, options).then((res) => res.json());
    } *// Return the cached promise*    return fetchMap[url];
  };
};
```

这个`createFetch`函数将为您创建一个缓存的`fetch`。如果你用同一个 URL 调用它两次，它将返回相同的承诺。所以你可以这样制作一个新的`fetch`:

```
*const* myFetch = *createFetch*();
```

然后用它在你的`useEffect`中代替`fetch`用一个简单的替换:

```
 const [people, setPeople] = useState([]);
  useEffect(() => {
    **myFetch**("/people").then(setPeople);
  }, []);
```

这就是为什么会这样。第一次调用`useEffect`时`myFetch`启动`fetch`并将承诺存储在`fetchMap`中。然后第二次调用`useEffect`函数时，`myFetch`函数返回缓存的承诺，而不是再次调用`fetch`。

如果您选择使用这种方法，那么这里唯一需要解决的问题就是缓存失效。

# 修复 5:使用反应查询

如果您使用 [React-Query](https://react-query.tanstack.com/) ，这些都不是问题。React-Query 是一个神奇的库，无论如何你都应该诚实地使用它。从 React-Query 开始，首先安装`react-query` NPM 包。

从那里创建一个查询客户端，并将您的应用程序包装在一个`QueryProvider`组件中:

```
*import* { **QueryClient**, **QueryClientProvider**} *from* "react-query";...const AppWithProvider = () => (
 **<QueryClientProvider client={new QueryClient()}>**    <App />
 **</QueryClientProvider>** );
```

然后在你的组件中使用`useQuery`钩子，像这样:

```
 const { data: people } = useQuery("people", () =>
    fetch("/people").then((res) => res.json())
  );
```

那不是看起来更好吗？它不做双重提取。

这只是 React-Query 所能做的事情的一小部分。人们使用 React-Query 不仅仅是为了获取数据，还可以用它来监控任何基于承诺的异步工作。

# 修复 6:使用状态管理器

我不打算在这一点上进入代码细节，因为它很大程度上取决于您使用的状态管理器。但是如果你使用 Redux，那么如果你使用 Redux 工具包中的 [RTK 查询功能](https://redux-toolkit.js.org/rtk-query/overview)，你将不会受到这种双重挂载行为的影响。

# 你不应该做什么

我强烈建议不要使用`useRef`来试图击败这种行为。不能保证第一次`useEffect`调用的组件就是第二次调用的组件。所以如果你做一些事情，比如使用`useRef`在坐骑之间进行追踪，那么……不清楚这是否可行。

此外，当前用来创建`useEffectOnce`的代码也不起作用。它不调用清理函数。这比调用两次`useEffect`要糟糕得多。

# 你应该做什么

如果你喜欢这个内容，你应该看看我的 [YouTube 频道](https://www.youtube.com/c/JackHerrington)。我一直在报道这样的话题。事实上，我已经在那边讲过了`[useEffect](https://youtu.be/j8s01ThR7bQ)` [主题，但是我还没有具体讲过 API 调用方面…还没有。](https://youtu.be/j8s01ThR7bQ)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***