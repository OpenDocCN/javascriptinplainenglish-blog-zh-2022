# 2022 年后端开发者学习 React 的最短教程

> 原文：<https://javascript.plainenglish.io/the-shortest-tutorial-to-learn-reactjs-for-a-backend-developer-in-2022-part-1-bd7aa96182ed?source=collection_archive---------3----------------------->

## 第 1 部分:React 的 3 个核心维度——`basic concepts`、`components`、`Hooks —` 帮助你快速掌握 React

![](img/51028ef8cea8787bc4b6cc918049533c.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/es/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为开发人员，我们总是想学习新的东西。作为后端开发人员，我们只需要扩展视野，不要只关注我们已经熟悉的小领域。

React，世界上最流行的 UI 框架非常庞大，需要很长时间才能学会。如果你是一个 React 老手，你也可以检查一下缺口，留着以后用。我相信阅读这篇文章会比浏览 React 文档或搜索来解决问题要快得多。

本文试图从初学者的角度，围绕 React 的三个核心维度:`basic concepts`、`components`、`Hooks`，讲解 React 中 90%以上的实用特性和常用概念，帮助你快速掌握 React。

让我们开始最短的旅程。

# **1。初始化项目**

## **1.1 安装**

开发 web 应用时，`React`通常需要与`ReactDOM`配合使用，下面是使用`npm`安装`React`的命令。

```
npm i react react-dom
```

## **1.2 使用** `**CRA**`创建项目

创建 React 项目的最快方法是使用 Create-React-App(简称 CRA)。

```
npx create-react-app APP_NAME
```

# **2。基本概念**

## **2.1 元素**

React 元素的编写方式与普通 HTML 元素相同，您可以使用 HTML 语法在 React 中创建任何元素。

```
<div>I'm JSX</div>
```

这个语法叫做`JSX`。实际上，`JSX`语法只是 JavaScript 的语法糖，所以仍然需要使用像`babel`这样的工具来编译。与 HTML 不同，JSX 的自结束标签必须用斜线结束。

```
<img src="/img.png" />
```

## **2.2 元素属性**

除了元素的语法略有不同之外，JSX 和 HTML 在元素属性方面也有细微的区别。
由于 JSX 是 JavaScript，JavaScript 中的命名约定是使用 camel 命名，所以 JXS 中的所有元素属性都要改用 camel 命名(事件也一样)。

```
<input defaultChecked defaultValue="o" onInput={()=>{}} />
```

除了正常属性之外，还有一个特殊属性需要注意。

这个特殊的属性是 class，因为在 JavaScript 中，class 是一个关键字，所以需要使用 className 来代替。

```
<div className="class"></div>
```

## **2.3 元素样式**

在 JSX 使用内联样式时，我们不应该使用字符串，而应该使用对象。

```
<div style={{ fontSize: '1.25rem', textAlign: 'center' }}>**Hello**, JSX</div>
```

## **2.4 组件**

我们可以将多个元素组合成一个 React 组件。
以前编写组件的 React 方式是使用类，现在更推荐的方式是使用函数。函数组件类似于普通函数，但有两个不同之处:

*A .组件名称以大写字母开头。组件需要返回 JSX 元素。*

这是最简单的组件之一。

```
function MyComponent() {
  return <div>Hello Component!</div>
}
```

## **2.5 片段**

React 要求所有组件都应该有一个根元素，这意味着一个组件不能同时包含多个同级元素。
下面是一个反例，它会认为是语法错误:

```
function Sign() {
  return (
    <input />
    <input />
    <button />
  )
}
```

在 React 16.2.0 之后，JSX 提供了片段组件来处理这种情况。

我们可以这样写:

```
function Sign() {
  return (
    <React.Fragment>
      <input />
      <input />
      <button />
    </React.Fragment>
  )
}
```

`Fragment`也可以缩写为`<></>`，所以我们一般是这样写的。

```
function Sign() {
  return (
    <>
      <input />
      <input />
      <button />
    </>
  )
}
```

## **2.6 道具**

组件可以相互环绕，从而形成父子关系。

```
<Parent>
  <Child />
</Parent>
```

我们可以将数据传递给父组件中的子组件，我们称之为`props`。传递属性的语法与普通属性相似，但不同之处在于可以传递对象。

```
<**Child** name='Mary', age={19} />
```

属性是通过函数的参数在子组件中接收的。JavaScript 中的变量在组件中使用时是用括号括起来的。

```
function Child(props) {
  return <div>
    <span>{props.name}</span>
    <span>{props.age}</span>
  </div>
}
```

我们还可以用对象解构的语法使代码更简单。

```
function Child({ name, age }) {
  return <div>
    <span>{name}</span>
    <span>{age}</span>
  </div>
}
```

如果你想把当前所有的道具传递给子组件，有一个简单的方法。

```
function Parent(props) {
  return <Child {...props} />
}
```

这将把父对象的所有道具传递给子对象。

## **2.7 儿童**

我们可以在组件内部放置其他元素或组件。
以这种方式放在中间的元素或组件称为子元素。

嵌入的元素或组件安装在 props 对象上，我们可以通过 props.children 访问子组件。

```
<Parent>
  <Child />
</Parent>function Parent({children}) {
  return children // children equals to <Child />
}
```

## **2.8 条件渲染**

React 可以根据特定条件选择显示或隐藏哪些内容。

最简单的方法是使用 if 语句。

```
function App() {
  const { isLoading, isError, data } = fetchData()  
  if(isError) {
    return <Error />
  }
  if(isLoading) {
    return <Loading />
  }
  return <div>{data}</div>
}
```

如果您在组件嵌套中使用条件，您将需要使用三元运算符，这些运算符需要包含在括号中。

```
function App() {
  const { isLoading, isError, data } = fetchData()
  return (<Layout>
      {
        isError ? <Error />:
        isLoading ? <Loading />:
          <div>{data}</div>
      }
    </Layout>)
}
```

除了三元运算符之外，短路运算符在某些情况下也可用于提高可读性。

```
function App() {
  const { isLoading, isError, data } = fetchData()
  return (<Layout>
      {isError && <Error />}
      {isLoading && <Loading />}
      <div>{data}</div>
    </Layout>)
}
```

## **2.9 列表效果图**

我们还可以将数据列表呈现到组件中。

渲染 React 组件最常见的方式是通过数组的 map 方法。

```
const users = ['Mary', 'Lucy', 'Jack']function App() {
  return (
    <>
      {users.map(user => <div key={user}>{user}</div>)}
    </>
  )
}
```

注意，当我们进行列表呈现时，我们需要为每个元素设置一个键，并且这个键必须保持唯一。

## **2.10 HTML 字符串渲染**

当我们已经有一个 HTML 字符串时，我们需要将它直接呈现到页面上。

在 React 中实现这一点的方法是使用`dangerouslySetInnerHTML`属性，该属性接受一个对象的值，该对象的`__html` 属性被设置为 HTML 字符串。

```
const htmlString = '<p>I'm HTML String</p>'<div dangerouslySetInnerHTML={{ __html: htmlString }}></div>
```

## **2.11 上下文**

当我们的组件嵌套层次太深时，在相距太远的两个组件之间传递道具可能会很麻烦，我们需要让中间的所有组件都接收它们一开始就不使用的道具。

```
function App() {
  const username = 'Mary'
  return <Layout username={username}>
    <div>Hello</div>
  </Layout>
}// Layout receiving username is redundant
function Layout({ username }) {
  return <User username={username}></User>
}function User({ username }) {
  return <h1>{username}</h1>
}
```

为了解决这个问题，React 提供了上下文来允许我们的组件在 props 之外共享数据。上下文是使用 React 的 createContext 函数创建的，该函数返回一个具有两个属性的上下文对象，`Provider`和`Consumer`，这两个属性都是组件。

我们使用`Provider`组件包装需要传递数据的根组件，然后在需要使用数据的位置用`Consumer`组件包装它以获取数据。

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
  return <UserNameContext.Consumer>
    {username => <h1>{username}</h1>}
  </UserNameContext.Consumer>
}
```

在使用上下文之前，我们需要考虑组件的设计是否正确。

今天，我们只讨论 React 的基本概念。在我们的下一篇文章中，我们将开始讨论 React 的`components`。让我们期待吧。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***