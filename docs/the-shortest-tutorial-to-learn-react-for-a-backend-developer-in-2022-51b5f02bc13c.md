# 2022 年后端开发者学习 React 的最短教程

> 原文：<https://javascript.plainenglish.io/the-shortest-tutorial-to-learn-react-for-a-backend-developer-in-2022-51b5f02bc13c?source=collection_archive---------1----------------------->

## 第 3 部分:React 的 3 个核心维度——基本概念、组件和挂钩——帮助您快速掌握 React

![](img/8d8e230e7339ea46e3d48877a1b2b5d7.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为开发人员，我们总是想学习新的东西。作为后端开发人员，我们只需要扩展视野，不再只关注我们已经熟悉的小领域。

React，世界上最流行的 UI 框架非常庞大，需要很长时间才能学会。如果你是一个 React 老手，你也可以检查一下缺口，留着以后用。我相信阅读这篇文章会比浏览 React 文档或搜索来解决问题要快得多。

本文试图从初学者的角度，围绕 React 的三个核心维度:`basic concepts`、`components`、`Hooks`，讲解 React 中 90%以上的实用特性和常用概念，帮助你快速掌握 React。

让我们开始最短的旅程。

这是本文的“第 3 部分”。如果你想知道“第一部分”或“第二部分”，这里有一个列表:

[**2022 年后端开发者学习 ReactJs 的最短教程(第一部分:基础概念** )](/the-shortest-tutorial-to-learn-reactjs-for-a-backend-developer-in-2022-part-1-bd7aa96182ed)

[**2022 年后端开发者学习 ReactJs 的最短教程(第二部分:组件)**](https://medium.com/@malvin.lok/the-shortest-tutorial-to-learn-reactjs-for-a-backend-developer-in-2022-part-2-524182a11741)

# 4.钩住

React 16.8 版本之后，React 提供了`Hooks`机制，允许你用`state`创建功能组件，而不是用笨重的`Classes`创建组件。当今世界，我们应该避免使用`Class`组件，拥抱`Hooks`组件。

钩子有几个规则:

*   钩子以前缀开始:`use`
*   只能在 React 函数组件中使用
*   只能在 React 函数组件的顶层使用
*   不能有条件地使用

我们来解释一下 React 中的几个钩子。

*   使用状态
*   使用效果
*   useRef
*   使用上下文
*   使用回调
*   使用备忘录
*   用户教育
*   useLayoutEffect

## 4.1 使用状态

对外传递的数据称为`props`，组件的数据称为`state`。

可以使用`useState`创建状态。

`state`和普通变量的区别在于，当`state`改变时，组件将被重新渲染。

`useState`的用法如下:

```
**const** [stateValue, setStateValue] = **useState**(initialValue);
```

调用它需要传递一个初始值；它返回一个包含两个元素的数组，第一个是当前状态，第二个是更新状态的函数。

当我们调用更新状态的函数时，组件将被重新呈现。

下面举一个计数器的例子来理解`useState`的实际用法:

```
import { useState } from 'react'function Counter() {
  const [count, setCount] = useState(0)
  return <button onClick={()=> setCount(count+1)}>count: {count}</button>
}
```

## 4.2 使用效果

如果我们需要与组件外部的东西交互，我们需要使用`useEffect`，比如后端接口。

`useEffect`顾名思义，执行副作用，是存在于我们程序之外的操作，没有可预测的结果。

`useEffect`有两个参数，第一个是副作用函数，第二个是依赖项数组。每当依赖性数组改变时，副作用函数被重新执行。

```
**useEffect**(() => {}, [])
```

下面是一个从博客获取帖子列表数据的示例:

```
import { useEffect } from 'react';function PostList() {
  const [posts, setPosts] = useState([]); useEffect(() => {
    fetch('[https://yourblog.com/posts'](https://jsonplaceholder.typicode.com/posts'))
       .then(response => response.json())
       .then(posts => setPosts(posts));
   }, []); return posts.map(post => <div key={post.id}>{post.title}</div>)
}
```

## 4.3 用户参考

`useRef`的主要用途之一就是访问元素。

使用`useRef`就像调用它一样简单，返回一个值，并通过`props`将该值传递给 React 元素。

```
function MyComponent() {
  const ref = React.useRef(); return <div ref={ref} />
}
```

一旦`ref`被设置为一个元素，就可以通过`ref.current`访问它。

注意，在`ref`有值之前，必须等待组件完成渲染，否则`ref`是未定义的。

```
function MyComponent() {
  const ref = React.useRef();
  console.log(ref)// undefined

  useEffect(() => {
    console.log(ref.current) //now you can get it
  }, []) return <div ref={ref} />
}
```

最后，注意`refs`不能设置为组件，只能设置为元素。

如果我们想要访问组件内部的元素，我们可以使用`refs`来转发它们。

这通过以下方式实现:

*   使用`React.forwardRef.`包装函数组件函数组件的第二个参数是`ref`，它被设置为特定的元素。
*   使用`React.createRef`创建一个`ref`对象以设置到封装组件。

```
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

## 4.4 使用上下文

`useContext`是比仅仅使用`Context`更简单的使用`Context`的方法。

语法也很简单:调用`useContext`函数并将`Context`对象作为参数传递。

现在让我们重写原来的例子。

```
const UserNameContext = React.createContext('')function App() {
  const username = 'Mary'
  return <UserNameContext.Provider value={username}>
    <Layout>
    <div>Hello</div>
  </UserNameContext.Provider>
}function Layout() {
  return <User />
}function User() {
  const username = React.useContext(UserNameContext)
  return <h1>{username}</h1>
}
```

## 4.4 使用回调

`useCallback`的目的是提高性能。

如果我们在一个函数组件中创建了一些函数，那么每次重新渲染组件时都会重新创建这些函数，这可能会影响程序的性能。

`useCallback`有两个参数，第一个是要缓存的函数，第二个是依赖项数组。当依赖数组中的任何值改变时，`useCallback`重新创建函数。

此外，如果这些函数作为参数传递给子组件，将导致子组件被重新呈现。我们可以结合使用`memo`和`useCallback`来减少子组件的渲染。

```
function Button ({ onClick }) {
  console.log("button render");
  return <button onClick={onClick}>count++</button>;
};const MemoButton = React.memo(Button);function Counter() {
  const [count, setCount] = React.useState(0);

  const onClick = React.useCallback(() => {
    setCount((count) => count + 1);
  }, []);return (
    <>
      <p>count:{count}</p>
      <MemoButton onClick={onClick} />
    </>
  );
}ReactDOM.render(<Counter />, document.getElementById('app'));
```

## 4.5 使用备忘录

`useMemo`和`useCallback`的作用相似，也用于提高性能。区别在于`useCallback`是缓存的函数，而`useMemo`是缓存的值。

渲染所需的一些变量需要计算，计算的过程可能是非常性能密集型的，因此当组件被重新渲染并且计算所需的状态没有改变时，可以再次避免。

与`useEffect`和`useCallback`类似，`useMemo`将在其依赖关系改变时重新计算值。这里有一个例子，说明如何将其应用于`useCallback`中的例子。添加了`UserInfo`组件，因此当`Counter`组件中的计数改变时，`UserInfo`不会随之更新。

```
function Button ({ onClick }) {
  console.log("button render");
  return <button onClick={onClick}>count++</button>;
};const MemoButton = React.memo(Button);function UserInfo({ userInfo: { name, age } }) {
  console.log('UserInfo render')
  return <div>
    <p>{name}</p>
    <p>{age}</p>
  </div>
}const MemoUserInfo = React.memo(UserInfo)function Counter() {
  const [count, setCount] = React.useState(0);
  const [name, setUsername] = React.useState('Mary');

  const onClick = React.useCallback(() => {
    setCount((count) => count + 1);
  }, []);

  const userInfo = React.useMemo(() => {
    return {
      name,
      age: 15
    }
  }, [name])return (
    <>
      <MemoUserInfo userInfo={userInfo} />
      <p>count:{count}</p>
      <MemoButton onClick={onClick} />
    </>
  );
}ReactDOM.render(<Counter />, document.getElementById('app'));
```

## 4.6 用户

`useReducer`是替代`useState`的钩子，用于处理复杂的状态逻辑。

如果你用过`redux`，你会很熟悉。

它需要两个参数，第一个是`reducer`，第二个是初始状态。

它返回一个包含两个元素的数组，第一个元素是当前状态，第二个元素是改变状态的调度函数。这与 useState 非常相似。

`reducer`是一个带两个参数的函数，当前的`state`和用于改变`state`的`action`，并返回新的`state`。

```
onst initialState = 0const reducer = (state, action) => {
  switch (action) {
    case 'increment':
      return state + 1
    case 'decrement':
      return state - 1
    case 'reset':
      return initialState
    default:
      return state
  }
}function Counter() {
  const [count, dispatch] = React.useReducer(reducer, initialState)
  return (
    <div>
      <div>Count: {count}</div>
      <button onClick={() => dispatch('increment')}>ADD</button>
      <button onClick={() => dispatch('decrement')}>DECREASE</button>
      <button onClick={() => dispatch('reset')}>RESET</button>
    </div>
  )
}ReactDOM.render(<Counter />, document.getElementById('app'));
```

## 4.7 使用延迟效果

`useLayoutEffect`和`useEffect`的唯一区别是执行的时间不同。`useLayoutEffect`是在浏览器完成绘制和布局后执行的，所以`useLayoutEffect`可以防止页面闪烁。

最常见的一种情况就是`state`更新一次，触发效果的回调函数再次更新`state`，导致短时间内连续两次`state`更新。这可以通过使用下面的主动截止时间倒计时程序来理解。

```
function useInterval(callback, delay) {
  const savedCallback = React.useRef();React.useEffect(() => {
    savedCallback.current = callback;
  });React.useEffect(() => {
    function tick() {
      savedCallback.current();
    }
    if (delay !== null) {
      let id = setInterval(tick, delay);
      return () => clearInterval(id);
    }
  }, [delay]);
}function Draw() {
  const [countdown, setCountdown] = React.useState(3) useInterval(()=> setCountdown(countdown - 1), 1000)

  React.useLayoutEffect(() => {
    if(countdown <= 0) {
      setCountdown(3)
    }
  }, [countdown])
  return (
    <div>
      <div>deadline countdown：{countdown} s</div>
    </div>
  )
}ReactDOM.render(<Draw />, document.getElementById('app'));
```

活动倒计时每秒减少 1 秒，当减少到 0 秒时重置为 3 秒。

如果在倒计时设置为 0 时使用`useEffect`，页面会重新渲染，倒计时会立即再次设置为 3，导致页面在很短的时间内渲染两次。

`useLayoutEffect`在很多场景下不使用，而且会阻碍渲染。这通常可以通过业务逻辑来避免。

## 4.8 自定义`Hook`

我们可以根据需要定制`Hook`，`Hook`用于逻辑复用。

定制`Hook`时有几个条件需要注意:

*   钩子是一个以`use`开始的函数。
*   其他的`Hook`可以在函数内部调用

`useLayoutEffect`中的例子使用了自定义`Hook`“使用间隔”:

```
function useInterval(callback, delay) {
  const savedCallback = React.useRef(); // saving the new callback
  React.useEffect(() => {
    savedCallback.current = callback;
  }); // establish interval
  React.useEffect(() => {
    function tick() {
      savedCallback.current();
    }
    if (delay !== null) {
      let id = setInterval(tick, delay);
      return () => clearInterval(id);
    }
  }, [delay]);
}
```

就是这样。当你作为后端工程师第一次尝试学习 React 时，这里有三个关于 React 的基本概念。

但是我知道，当你看到这篇文章的时候，你会承认，尤其是关于钩子的第三部分。不过没关系，你可以慢慢来。把这篇文章当作一个小字典，当你看到一些你不知道的东西或者你想知道的东西时，请便，用你今天学到的术语搜索更多的信息。

我叫马尔文，是一名后端开发者，想成为全栈开发者。

下次见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***