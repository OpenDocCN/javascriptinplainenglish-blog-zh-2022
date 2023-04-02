# React 中的“记忆化”是什么

> 原文：<https://javascript.plainenglish.io/what-is-memoization-in-react-50c2d6f4f71e?source=collection_archive---------23----------------------->

## 用这两个有用的钩子优化 React 代码。

内存化是一种缓存计算结果(或函数本身)以优化性能的方法。例如，如果列表的结果已经更改，您可能只想重新呈现列表元素，或者如果另一个值已经更改，您可能只想更改一个值。

需要注意的是，react 默认情况下会尝试这样做，而且在大多数情况下，react 的默认差异就足够了。记忆化实际上应该只在需要性能提升或者有特殊需求的项目中使用。

![](img/b58b5880273b4c478540e983a503ef65.png)

## 我如何记忆？

在记忆反应中有两个“钩子”。一个是[【使用备忘录】](https://reactjs.org/docs/hooks-reference.html#usememo)，另一个是[使用回调](https://reactjs.org/docs/hooks-reference.html#usecallback)。本质上，它们做同样的事情，但是 useMemo 保存一个结果(字符串、数字、HTML ),而 useCallback 保存一个函数。我不能说我完全理解 useCallback 的命名——在我看来，它应该更明确一些，比如“use**Memo**Callback”——但我不是脸书的明星开发人员😅。

例如，假设您想要将计算结果保存在正在渲染的组件中。你可以根据 React [文档](https://reactjs.org/docs/hooks-reference.html#usememo')用 useMemo 来完成:

```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

这个钩子末尾的数组是依赖项的列表。这些值如果发生变化，将告诉 react 组件在下次渲染时重新计算该值。因此，如果 a 或 b 发生了变化，显然需要重新计算值，否则用户将在 UI 中看到一个过时的值。

在组件的上下文中，您可能会看到类似这样的内容([查看这里的示例代码](https://codesandbox.io/s/factorial-with-memoization-65mkk?file=/src/App.js)):

在上面的例子中，如果您要分析 JavaScript 代码执行的速度，第一次渲染可能需要几十毫秒的时间，而单击“rerender”按钮后触发的渲染将更接近 1，甚至更快。这是因为 useMemo 钩子将在第一次调用该函数时保存该值，而不会在第二次重新运行计算。

`useCallback`与 useRef 相同，但它缓存的是函数而不是值。你可能想确保你的函数不会在每次渲染时被不必要的重新创建。如果您在 useCallback 调用中包装您的方法，那么它的行为将与 useMemo 相同，被缓存并仅在依赖关系改变时重新计算。

例如:

```
const [counter, setCounter] = useState(0)
let func2 = useCallback(() => { let c = counter; return <p> useCallback function is processing the value <b>{c}</b> in the count variable </p>}, [counter])
```

在这个例子中，函数闭包将为输入“c”保存一个静态值，只有当该值改变时，函数才会被重新计算。如果您将一个空数组传递给 useCallback 方法，那么 c 的值永远不会改变，并且该函数只会处理计数器的第一个值。

感谢阅读，

~亚历克斯

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**