# 2 个有用的 React 挂钩:useReducer 和 useContext

> 原文：<https://javascript.plainenglish.io/2-useful-react-hooks-usereducer-and-usecontext-2fbb6461a5c?source=collection_archive---------11----------------------->

## React 中两个有用的钩子

![](img/9be195ca153170cc03640228a1ed44df.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

useReducer 和 [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext) 是 React 中管理本地和全局状态的两个有用的钩子。

使用 useContext，您可以操纵全局状态，并从不同组件访问它，而无需钻取，将状态传递到多个层。

下面的示例展示了实际使用的 useReducer，将 action 关键字作为一个参数，将当前状态作为另一个参数。

要更新状态，最好创建现有状态的副本，然后用更新的值覆盖它。使用对象析构是使用 Reacts useReducer 钩子的方法，但是有一些库可以使它更简单，比如 useImmer。

```
function reducer(state, action) { const prevState = { ...state }; console.log(state, action); switch (action.type) { case 'increment': return { ...state, count: prevState.count + 1 }; case 'decrease': return { ...state, count: prevState.count - 1 }; default: return { ...state }; }}
```

为了访问状态并更新它，useContext 是一个很好的钩子，它可以很好地与 useReducer 钩子协同工作。

初始状态存储在对象中，可以使用 reducer 进行更新。更新后的状态将被传递给 useReducer 钩子。

```
const initialState = {title: 'Hello',count: 1,loggedIn: false,};
```

在下面的示例中，StateContext 用于存储当前状态，DispatchContext 用于更新全局状态。

```
const [state, dispatch] = useReducer(reducer, initialState);
```

状态值是 StateContext 的当前值，调度用于更新这些值。

```
return (<StateContext.Provider value={state}><DispatchContext.Provider value={dispatch}><h1>App.js Count: {state.count}</h1><p>Start editing to see some magic happen!! :)</p><Test /></DispatchContext.Provider></StateContext.Provider>);
```

要访问测试组件中的全局状态，首先要导入上下文提供者。

```
import DispatchContext from '../DispatchContext';import StateContext from '../StateContext';
```

要访问状态，请使用挂钩 useContext:

```
const appState = useContext(StateContext);
```

要访问调度方法，请执行以下操作:

```
const appDispatch = useContext(DispatchContext);
```

要更新全局状态中的计数值:

```
function decrease() { appDispatch({ type: 'decrease' });}
```

App.js 中的 reducer 方法将被通知来自 Test.js 的调度事件，并更新状态。

# 源代码

【https://stackblitz.com/edit/react-fdyiu8?file=src/App.js 

# 试映

[https://react-FDY iu8 . stack blitz . io](https://react-fdyiu8.stackblitz.io)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***