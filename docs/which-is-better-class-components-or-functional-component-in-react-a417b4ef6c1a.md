# 哪个更好？React 中的类组件还是功能组件？

> 原文：<https://javascript.plainenglish.io/which-is-better-class-components-or-functional-component-in-react-a417b4ef6c1a?source=collection_archive---------0----------------------->

## React 中功能组件和类组件的区别。

![](img/1bd96e18349221683e3cb9f13d9aefe7.png)

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我开始我的 React 项目时，我的第一个问题是使用类组件还是功能组件。另一种选择是在项目中同时使用这两者。我希望每个人都在他们的项目中使用这两种组件。

> *React 允许您将组件定义为类或函数。*

在找到更好的选择之前，我们将创建类组件和功能组件。

> 创建 React 组件时，组件名必须以大写字母开头。

## 类别组件

要定义 React 组件类，您的类需要用`React.Component`扩展。

必须在类组件中定义`render()`方法。其他`React.Component`方法可选，如`constructor()` `componentDidMount()`等。

```
class Hello extends React.Component {
  render() {
    return <h1>Hello World!</h1>;
  }
}

const element = <Hello />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/eYGrwdw)

## 功能成分

这里我们要把上面的类组件变成一个功能组件。

```
function Hello() {
  return <h1>Hello World!</h1>;
}

const element = <Hello />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

功能组件易于编写，代码更少，更容易理解。因为它只是一个返回 JSX 的普通 JavaScript 函数。

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/BawxgWr)

# 功能组件和类组件的区别

我们讨论了类组件和功能组件之间的每个区别。

*   1.组件渲染
*   2.搬运道具
*   3.处理状态
*   4.生命周期方法
*   5.访问组件子项
*   6.高阶组件
*   7.误差边界

## 1.组件渲染

在类组件中，`render()`方法用于通过扩展 `React.Component`来渲染 JSX

功能组件只是一个返回 JSX 的普通 JavaScript 函数。

前两个程序是组件呈现的完美例子。

```
// Class component
class Hello extends React.Component {
  render() {
    return <h1>Hello World!</h1>;
  }
}

//Function component
function Hello() {
  return <h1>Hello World!</h1>;
}

//Function component with Arrow function
Hello = () => {
  return <h1>Hello World!</h1>;
}
```

**获胜者:功能组件**

通过使用[箭头功能](https://medium.com/swlh/es6-arrow-functions-in-javascript-54f244f6c7cd)，功能组件的创建更加简单。普通的 JavaScript 函数被用作功能组件。没有更多的渲染方法。

[](https://balajidharma.medium.com/difference-between-es6-arrow-functions-and-regular-functions-in-javascript-4ba4fcb5d352) [## ES6 箭头函数和 JavaScript 中常规函数的区别

### 箭头函数与常规函数

balajidharma.medium.com](https://balajidharma.medium.com/difference-between-es6-arrow-functions-and-regular-functions-in-javascript-4ba4fcb5d352) 

## 2.搬运道具

`props`代表属性，并被传递给 React 组件。它还用于将数据从一个组件传递到另一个组件。阅读更多官方 [React 文档](https://reactjs.org/docs/components-and-props.html)。

**带道具的类组件**

`this.props`用于访问我们的`name`道具。

```
class Hello extends React.Component {
  render() {
    return <h1>Hello {this.props.name}!</h1>;
  }
}

const element = <Hello name="World"/>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/poWZGJb)

**带道具的功能组件**

有效的 React 函数组件应该有一个函数参数。`props`参数将拥有像`props.name`一样的所有组件道具。

```
function Hello(props) {
  return <h1>Hello {props.name}!</h1>;
}

const element = <Hello name="World" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/poWZjYB)

**获胜者:功能组件**

不用担心`this`关键字。语法简洁明了，它是赢家。

## 3.处理状态

`state`是 React 组件的内置对象，用于控制组件行为。当`state`对象改变时，组件将被重新渲染。

**状态为**的类组件

```
class Timenow extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return(
      <div>
        <h1>Hello {this.props.name}!</h1>
        <h2>Time Now {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

const element = <Timenow name="World"/>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/QWqBoXZ)

class components `constructor`方法用于初始化状态值。

**状态为**的功能组件

在功能组件中，使用 [useState](https://reactjs.org/docs/hooks-state.html) 钩子处理状态。

> *钩子*是 React 16.8 新增的。它们允许您使用状态和其他 React 特性，而无需编写类。

功能组件没有`this`，所以我们不能赋值或读取`this.state`。相反，我们在函数组件内部直接调用`useState`钩子。

```
function Timenow(props) {
  const [date, setDate] = React.useState(new Date());
  return (
    <div>
      <h1>Hello {props.name}!</h1>
      <h2>Time Now {date.toLocaleTimeString()}.</h2>
    </div>
  );
}

const element = <Timenow name="World" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/WNZKWNa)

**获胜者:功能组件**

使用`useState`挂钩完成`state`初始化。不需要`constructor`方法。

## 4.生命周期方法

在 React 中，每个组件都有几个`lifecycle`方法，这个方法帮助你在进程中的特定时间运行代码。[点击此处](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)查看 React 生命周期图。

**具有生命周期方法的类组件**

低于时钟类组件是实现生命周期方法的完美例子。

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/gaearon/pen/amqdNA)

**具有生命周期挂钩方法的功能组件**

我们使用`[useEffect](https://reactjs.org/docs/hooks-reference.html#useeffect)`钩子将上面的`clock`类组件转换成一个功能组件。

`useEffect`返回方法用于清理。

```
function Clock(props) {
  const [date, setDate] = React.useState(new Date());

  React.useEffect(() => {
    var timerID = setInterval(() => tick(), 1000);

    return function cleanup() {
      clearInterval(timerID);
    };
  });

  function tick() {
    setDate(new Date());
  }

  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {date.toLocaleTimeString()}.</h2>
    </div>
  );
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

在 CodePen 上试试

**获胜者:类别组件**

由于对所有生命周期方法使用相同的钩子，功能组件`useEffect`令人困惑。在类组件中，我们可以直接使用`componentDidMount`、`componentWillUnmount`等方法。

## 5.访问组件子项

特殊的`children`道具用于访问内容内部的组件或类似<布局>内容内部的组件</布局>。

**类组件**

`this.props.children`用于类组件。

```
class Layout extends React.Component {
  render() {
   return(
      <div>
        <h1>Hello {this.props.name}!</h1>
        <div>{this.props.children}</div>
      </div>
     );
  }
}

const element = <Layout name="World">This is layout content</Layout>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/XWexdmj)

**功能组件**

只是在功能组件中使用了`props.children`来访问孩子的内容。

```
function Layout(props) {
  return(
    <div>
      <h1>Hello {props.name}!</h1>
      <div>{props.children}</div>
    </div>
  );
}

const element = <Layout name="World">This is layout content</Layout>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/BawqKBv)

**获胜者:类别&功能组件**

两者都使用相同的`props.children`来访问组件的子组件。另外，我们需要使用`this`关键字。

## 6.高阶组件

高阶组件(HOC)是 React 中重用组件逻辑的一种高级技术。HOC 是一个纯函数，所以它只返回一个新的组件。

> 高阶分量是接受一个分量并返回一个新分量的函数。

**具有类组件的特设**

```
function classHOC(WrappedComponent) {
  return class extends React.Component{
    render() {
      return <WrappedComponent {...this.props}/>;
    }
  }
}

const Hello = ({ name }) => <h1>Hello {name}!</h1>;
const NewComponent = classHOC(Hello);

const element = <NewComponent name="World" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/NWaOrNb)

**带功能组件的特设**

```
function functionalHOC(WrappedComponent) {
  return (props) => {
    return <WrappedComponent {...props}/>;
  }
}

const Hello = ({ name }) => <h1>Hello {name}!</h1>;
const NewComponent = functionalHOC(Hello);

const element = <NewComponent name="World" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/dyVgXKy)

**获胜者:功能组件**

要创建 HOC，我们应该使用 JavaScript 函数(classHOC，functionalHOC)。[不要在渲染方法](https://reactjs.org/docs/higher-order-components.html#dont-use-hocs-inside-the-render-method)中使用 HOCs。在函数内部，我们可以使用类或功能组件。

## 7.误差边界

[错误边界](https://reactjs.org/docs/error-boundaries.html)是 React 组件，用于处理 React 组件中的 JavaScript 错误。因此，我们可以捕捉组件中的 JavaScript 运行时错误，并显示一个后备 UI。

> 错误边界是 React 组件，**捕捉子组件树中任何地方的 JavaScript 错误，记录这些错误，并显示一个回退 UI** 而不是崩溃的组件树。

如果使用了`[static getDerivedStateFromError()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)`或`[componentDidCatch()](https://reactjs.org/docs/react-component.html#componentdidcatch)`生命周期方法，就意味着类组件变成了一个错误边界。使用`static getDerivedStateFromError()`在抛出错误后呈现一个回退用户界面。使用`componentDidCatch()`记录错误信息。

错误边界作为一个 JavaScript `catch {}`块工作，但是对于组件。

有误差边界的简单例子

```
class ErrorCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {error: null, errorInfo: null};
  }

  componentDidCatch(error, errorInfo) {
    // Catch errors in any components below and re-render with error message
    this.setState({
      error: error,
      errorInfo: errorInfo
    })
    // You can also log error messages to an error reporting service here
  }

  refreshPage() {
    history.go(-1)
  }

  render() {
    if (this.state.errorInfo) {
      // Error path
      return (
        <div>
          <h2>Something went wrong.</h2>
          <details style={{ whiteSpace: 'pre-wrap' }}>
            {this.state.error && this.state.error.toString()}
            <br />
            {this.state.errorInfo.componentStack}
          </details>
          <hr />
          <button onClick={this.refreshPage}>
            Refresh Page
          </button>
        </div>
      );
    }
    // Normally, just render children
    return this.props.children;
  }
};
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(({counter}) => ({
      counter: counter + 1
    }));
  }

  render() {
    if (this.state.counter === 3) {
      // Simulate a JS error
      throw new Error('I crashed!');
    }
    return(
      <div>
        <h1>{this.state.counter}</h1>
        <button onClick={this.handleClick}>+</button>
      </div>
    );
  }
}

ReactDOM.render(
  <ErrorCounter>
    <Counter />
  </ErrorCounter>,
  document.getElementById('root')
);
```

[在 CodePen 上试试](https://codepen.io/balajidharma/pen/eYGQxJY)

**获胜者:类组件**

目前，只有类组件可以是错误边界。

# 结论:哪个更好？

如今，大多数应用程序都使用功能组件，因为它们简单、易用、易于理解。还有，在 React [v16.8](https://reactjs.org/docs/hooks-intro.html) 中引入钩子之后，功能组件变得非常有名。

由于钩子，功能组件中的生命周期方法易于使用。

对于没有介绍类的 ES6 JavaScript 背景的新手来说，类组件很难理解。

与 Java、PHP 和 C#等其他编程语言不同，JavaScript 类是原型继承之上的语法糖。换句话说，ES6 类只是特殊函数。所以我们不能在 JavaScript 类中使用类特性。

类组件在错误处理中起着重要的作用。因为类组件只支持错误边界生命周期方法`[static getDerivedStateFromError()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)`或`[componentDidCatch()](https://reactjs.org/docs/react-component.html#componentdidcatch)`。

没有更好的了，因为两者都有利弊。但是类组件对于理解 React 流和生命周期方法很重要。

新学员应该使用课程组件练习 React。一旦他们熟悉了类组件，他们就可以学习和使用功能组件。

感谢您的阅读！请随意评论您的反馈，并分享类组件和功能组件之间缺失的差异。

**参考文献**

```
[https://reactjs.org/docs/react-component.html](https://reactjs.org/docs/react-component.html)[https://reactjs.org/docs/components-and-props.html](https://reactjs.org/docs/components-and-props.html)[https://reactjs.org/docs/state-and-lifecycle.html](https://reactjs.org/docs/state-and-lifecycle.html)[https://reactjs.org/docs/higher-order-components.html](https://reactjs.org/docs/higher-order-components.html)[https://www.twilio.com/blog/react-choose-functional-components](https://www.twilio.com/blog/react-choose-functional-components)[https://blog.logrocket.com/handling-javascript-errors-react-error-boundaries/](https://blog.logrocket.com/handling-javascript-errors-react-error-boundaries/)
```

## 进一步阅读

[](https://bit.cloud/blog/composable-link-component-that-works-in-any-react-meta-framework-l7i3qgmw) [## 可在任何 React 元框架中工作的可组合链接组件

### Bit 的链接组件是一个与运行环境无关的组件。您可以将此链接用于…

比特云](https://bit.cloud/blog/composable-link-component-that-works-in-any-react-meta-framework-l7i3qgmw) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*