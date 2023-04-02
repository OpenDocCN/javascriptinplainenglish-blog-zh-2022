# 提高效率和可维护性的 7 个必备 React 挂钩

> 原文：<https://javascript.plainenglish.io/7-must-know-react-hooks-for-improved-efficiency-and-maintainability-a39fe7c0656e?source=collection_archive---------5----------------------->

我的日常发展行动挂钩

作为一名软件工程师，我发现 React 挂钩是一个改变游戏规则的工具，可以为功能组件添加状态和其他 React 特性。在这篇博文中，我将分享我认为每个开发人员都应该熟悉的七个 React 挂钩。这些钩子为我节省了无数的编码时间，并使我的 React 应用程序更加高效和可维护。所以，让我们深入了解一下这些强大的钩子吧！

![](img/7587f7358dde6cbef5e6a20f502badc5.png)

[Get the hook. Get it?](https://forum.wordreference.com/threads/get-the-hook-get-it.3283268/)

## 使用状态

useState 钩子是最基本和最重要的 React 钩子。它允许功能组件拥有状态，这对于管理和更新 React 应用程序中的数据至关重要。useState 挂钩将初始状态值作为参数，并返回包含两个元素的数组:当前状态值和更新状态值的函数。

```
const [count, setCount] = useState(0);

const increment = () => setCount(count + 1);
const decrement = () => setCount(count - 1);
```

## 使用效果

useEffect 钩子是一个通用的钩子，它允许功能组件执行副作用，比如数据获取、订阅和 DOM 更新。useEffect 挂钩将一个函数作为参数，并在每次渲染后执行它。它还带有一个可选的依赖数组，允许开发人员控制何时应该执行效果。

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

## 使用上下文

useContext 挂钩允许功能组件访问 React 上下文，这是一种通过组件树传递数据的方式，而不必在每一层手动传递属性。useContext 挂钩将一个上下文对象作为参数，并返回该上下文的当前上下文值。

```
const theme = useContext(ThemeContext);
```

## useRef

useRef 钩子允许功能组件访问底层 DOM 元素，这对于管理焦点、文本选择或媒体回放非常有用。useRef 钩子接受一个初始值作为参数，并返回一个可变的 Ref 对象，该对象可用于存储一个跨渲染持久的值。

```
const inputRef = useRef();

const focusInput = () => {
  inputRef.current.focus();
};
```

## 用户教育

useReducer 挂钩是 useState 挂钩的更高级版本，它允许功能组件管理复杂的状态逻辑，例如处理异步操作、数据加载和错误处理。useReducer 挂钩将 Reducer 函数和初始状态作为参数，并返回当前状态和可用于更新状态的调度函数。这个钩子对于以可预测和一致的方式管理复杂的状态特别有用。

```
const [state, dispatch] = useReducer(reducer, initialState);

dispatch({ type: 'increment' });
```

## 使用回调

useCallback 挂钩是一个性能优化挂钩，允许开发人员记忆昂贵的或经常使用的函数。useCallback 挂钩将一个函数和一组依赖项作为参数，并返回该函数的一个记忆版本，只有当其中一个依赖项发生变化时，该函数才会发生变化。这可以通过减少不必要的重新渲染次数来提高 React 应用程序的性能。

```
const memoizedCallback = useCallback(() => {
  doSomethingExpensive();
}, [dependencies]);
```

## 使用备忘录

useMemo 挂钩类似于 useCallback 挂钩，但它允许开发人员记忆复杂表达式的值，而不是函数的值。useMemo 钩子将一个函数和一组依赖项作为参数，并返回函数的记忆值，该值只在其中一个依赖项发生变化时才发生变化。这还可以通过减少不必要的计算来提高 React 应用程序的性能。

```
const memoizedValue = useMemo(() => {
  return expensiveComputation(param);
}, [param]);
```

总之，作为一名软件工程师，我发现 React Hooks 是我的工具箱中不可或缺的工具。这篇博文中讨论的七个钩子——useState、useEffect、useContext、useRef、useReducer、useCallback 和 use memo——极大地提高了我的 React 应用程序的效率和可维护性。我强烈建议所有开发人员熟悉这些挂钩，并将它们融入到自己的项目中。编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***