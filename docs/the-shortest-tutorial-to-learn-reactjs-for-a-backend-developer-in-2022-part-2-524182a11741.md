# 2022 年后端开发者学习 React 的最短教程

> 原文：<https://javascript.plainenglish.io/the-shortest-tutorial-to-learn-reactjs-for-a-backend-developer-in-2022-part-2-524182a11741?source=collection_archive---------3----------------------->

## 第 2 部分:React 的 3 个核心维度——基本概念、组件和挂钩——帮助您快速掌握 React

![](img/3e0c306740bbd47312ea4331fa86dd58.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为开发人员，我们总是想学习新的东西。作为后端开发人员，我们只需要扩展视野，不再只关注我们已经熟悉的小领域。

React，世界上最流行的 UI 框架非常庞大，需要很长时间才能学会。如果你是一个 React 老手，你也可以检查一下缺口，留着以后用。我相信阅读这篇文章会比浏览 React 文档或搜索来解决问题要快得多。

本文试图从初学者的角度，围绕 React 的三个核心维度:`basic concepts`、`components`、`Hooks`，讲解 React 中 90%以上的实用特性和常用概念，帮助你快速掌握 React。

让我们开始最短的旅程。

这是本文的“第 2 部分”。如果你想知道“第一部分”，这里有一个列表:

[**2022 年后端开发者学习 ReactJs 的最短教程(上)**](https://medium.com/@malvin.lok/the-shortest-tutorial-to-learn-reactjs-for-a-backend-developer-in-2022-part-1-bd7aa96182ed)

# **3。组件**

在`Basic Concepts`一章中提到了组件的概念，这里对组件有更详细更全面的解释。

## 3.1 组件`class`与组件`function`

React 中有两种类型的组件:`class`和`function`。

`class`是这样的:

```
class MyComponent extends React.Component {
  render() {
    return <div>hello</div>
  }
}
```

`class`组件需要从`React.Component`扩展并返回渲染方法中要渲染的 JSX。

而`function`就像是:

```
function MyComponent () {
  return <div>hello</div>
}
```

这两者的目的是一样的。

本文将重点介绍`function`组件。这是因为 React 的当前最佳实践是`function`组件。

## 3.2 纯成分

纯组件是一种性能优化，在道具和状态都没有变化的情况下，使用纯组件避免了无意义的渲染。纯组件是通过继承`React.PureComponent`实现的。

```
class MyComponent extends React.PureComponent {
  render(){
    return <div>I'm Pure Component</div>
  }
}
```

功能组件是通过`React.memo`实现的，T15 是 16.6.0 中加入 API 的高级组件。

```
function MyComponent() {
  return <div>I'm Pure Component</div>
}const PureComponent = React.memo(MyComponent)
```

## 3.3 为道具设置默认值

有时组件需要为 props 设置默认值，通常有两种方法。

**3.3.1 设置默认参数**

```
function MyComponent (props = { name: 'Mary' }) {
  return <div>hello { props.name }</div>
}
```

**3.3.2 设置** `**defaultProps**` **属性**

```
function MyComponent (props) {
  return <div>hello { props.name }</div>
}MyComponent.defaultProps = {
  name: 'Mary'
}
```

## 3.4 子组件触发传递给父组件的事件

虽然 React 中没有事件的概念，但是父组件可以传递一个函数给子组件，子组件在执行某个操作时触发这个回调函数，以参数的方式传递父组件需要的数据。

```
function App() {
  const submit = (data) => fetch('/api', { data })
  return <Form onSubmit={submit} />
}function Form({ onSubmit}) {
  const [data, setData] = useState()
  return <div>
      <button onClick={() => onSubmit(data)}>Submit</button>
    </div>
}
```

## 3.5 高阶组件

高阶组件(HOC)是一种重用组件逻辑的技术。一个组件把 props 转换成 UI，更高阶的组件把一个组件转换成另一个组件。使用特设解决了焦点问题，允许需要解决的问题集中在特设组件中。它不是一个 API，而是一种编程模式。它的工作方式是将一个组件作为参数，并返回一个生成新组件的函数。这是一个处理加载的高级组件。

```
function MyComponent (props) {
  return <div>hello { props.name }</div>
}function Loading () {
  return <div>loading...</div>
}function withLoading ({ children }) => {
  return ({ isLoading }) => {
    if(isLoading) return <Loading />
    return children
  }
}const WithLoging = withLoading(MyComponent)
```

## 3.6 门户组件

有时我们需要在父组件之外呈现一个子组件，比如开发一个全局提示或全局对话框。

这就是我们需要使用`createPortal`方法来实现的时候了。

```
function Modal({ children }) {
  return ReactDOM.createPortal(
    children,
    document.getElementById('root')
  )
}
```

## **3.7 克隆组件**

有时我们需要从一个样本组件克隆一个新的 React 组件。

这通常在开发复杂组件时使用。

我们不能改变组件的子组件，但是我们可以克隆它来改变原始组件的道具、键和样式。

```
function App({ children }) {
  const cloneChildren = React.cloneElement(children, {
    // we can change props in here.
  })
  return cloneChildren
}
```

## 3.8 验证组件

当我们将一个组件作为参数传递时，我们需要验证这个参数是一个 React 组件。

`React.isValidElement`这样做，返回一个布尔值。

```
function Wrap(children) {
  const isElement = React.isValidElement(children)
  // ...
}
```

## 3.9 渲染组件

我们可以在旧项目的一部分使用 React，而不是在整个项目中使用 React。例如，我们想在一个由`jQuery`开发的项目中增量使用 React。`ReactDOM`提供渲染功能。我们只需要找到一个 DOM 并在其上安装 React 组件。

```
const container = document.getElementById('container')
ReactDOM
  .render(<Component />, 
          container,
          () => { console.log('It works！') }
         )
```

React 18 最新的 API 是`createRoot`，由创建的根对象的 render 方法渲染。语法与以前的版本非常相似:

```
const root = ReactDOM.createRoot(container)root.render(<Component />)
```

## 3.10 卸载组件

由于可以将组件渲染到 DOM，所以需要一个相应的 API 从 DOM 中卸载 React 组件，这就是`unmountComponentAtNode`。

```
**unmountComponentAtNode**(container)
```

React 18 的最新 API 是`root.unmont`。

```
root.**unmont**()
```

就是这样。这是教程的第 2 部分，讲的是`Component`。我们总结了 10 个有用的用法。希望这些对你的日常发展有所帮助。

在接下来的旅程中，我们将关注 React 的另一个概念:钩子。下次见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***