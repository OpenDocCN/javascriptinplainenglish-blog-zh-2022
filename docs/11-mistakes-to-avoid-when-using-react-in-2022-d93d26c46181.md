# 在 2022 年使用 React 时要避免的 11 个错误

> 原文：<https://javascript.plainenglish.io/11-mistakes-to-avoid-when-using-react-in-2022-d93d26c46181?source=collection_archive---------0----------------------->

## React 开发中应该避免的一些常见错误。

![](img/8e244458a9128c84e25f67db576b7fc7.png)

Cover via freecoursesonline

随着 React 越来越流行，越来越多的 React 开发者在开发过程中遇到了各种各样的问题。

在本文中，我将根据我的实际工作经验，总结 React 开发中的一些常见错误，以帮助您避免一些错误。

如果你是刚开始使用 React，建议你好好看看这篇文章。如果您已经使用 React 开发项目，也建议您检查并填补空白。

读完这篇文章，你将学会如何避免这 11 个反应错误:

1.  呈现列表时，不要使用键。
2.  通过赋值直接修改状态值。
3.  将状态值直接绑定到输入的 value 属性。
4.  执行 setState 后直接使用 state。
5.  使用 useState + useEffect 时无限循环。
6.  忘记清理 useEffect 中的副作用。
7.  布尔运算符的使用不正确。
8.  未定义组件参数类型。
9.  将字符串作为值传递给组件。
10.  没有以大写字母开头的组件名称。
11.  元素的事件绑定不正确。

# 1.呈现列表时，不要使用键

# 🎀问题

当我们第一次学习 React 时，我们会根据文档中描述的方法呈现一个列表，例如:

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) => <li>{number}</li>);
```

渲染后，控制台会提示一个警告⚠️ `a key should be provided for list items`。

# 🎉解决方法

您只需要按照提示为每个项目添加`key`属性:

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number, index) => <li key={index}>{number}</li>);
```

`key`帮助 React 识别哪些元素发生了变化，比如被添加或删除。所以我们需要为数组中的每个元素设置一个唯一的`key`值。

对于`key`的值，最好设置为唯一值。在上面的例子中，`index`被用作`key`的值。官方不建议。列表的顺序会变，没有唯一值，也没有最后一招。在这种情况下，性能会下降。

# 📚证明文件

[React —基本列表组件](https://reactjs.org/docs/lists-and-keys.html#basic-list-component)

# 2.通过赋值直接修改状态值

# 🎀问题

在 React 中，状态不能直接赋值和修改，否则会导致难以修复的问题。示例:

```
updateState = () => {
  this.state.name = "Chris1993";
};
```

此时，编辑会提示警告⚠️:

```
Do not mutate state directly. Use setState().
```

# 🎉解决方法

类组件可以用`setState()`方法修改，功能组件可以用`useState()`修改:

```
*// ClassComponent：use setState()*
this.setState({ name: "Chris1993" });*// FunctionConponent：use useState()*
const [name, setName] = useState("");
setName("Chris1993");
```

# 📚证明文件

[反应—状态和生命周期](https://reactjs.org/docs/state-and-lifecycle.html) [反应—使用状态挂钩](https://reactjs.org/docs/hooks-state.html)

# 3.将状态值直接绑定到输入的值属性

# 🎀问题

当我们直接将`state`的值作为参数绑定到`input`标签的`value`属性时，会发现无论我们在输入框中输入什么，输入框的内容都不会改变。

```
export default function App() {
  const [count, setCount] = useState(0);
  return <input type="text" value={count} />;
}
```

这是因为我们使用 state 为默认值的状态变量赋给`<input>`的`value`，功能组件中的`state`只能被`useState`返回的`set`方法修改。所以解决方法也很简单，修改时使用`set`方法即可。

# 🎉解决方法

只需将一个`onChange`事件绑定到`<input>`，通过调用`setCount`对其进行修改:

```
export default function App() {
  const [count, setCount] = useState(0);
  const change = (val) => setCount(val.value);
  return <input type="text" value={count} onChange={change} />;
}
```

# 4.执行 setState 后直接使用 state

# 🎀问题

当我们通过`setState()`修改数据并立即得到新数据时，会出现数据还是旧数据的情况:

```
*// init state data*
this.state = { name: "Chris1993" };*// update state data*
this.setState({ name: "Hello Chris1993!" });
console.log(this.state.name); *// output: Chris1993*
```

我们可能会认为此时输入的`this.state.name`应该是`Hello Chris1993!`，结果却是`Chris1993`。

这是因为`setState()`是异步的。执行`setState()`时，真正的更新操作会放在异步队列中执行，下一个要执行的代码(即`console.log`这一行)是同步执行的，所以打印出来的`state`不是最新值。

# 🎉解决方法

只需把后续要执行的操作封装成一个函数作为`setState()`的第二个参数，这个回调函数会在更新完成后执行。

```
this.setState({ name: "Hello Chris1993!" }, () => {
  console.log(this.state.name); *// output: Hello Chris1993!*
});
```

现在输出了正确的内容。

# 5.使用 useState + useEffect 时出现无限循环

# 🎀问题

当我们在`useEffect()`中直接调用`useState()`返回的`set*()`方法，并且不设置`useEffect()`的第二个参数时，会发现一个死循环:

```
export default function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    setCount(count + 1);
  });
  return <div className="App">{count}</div>;
}
```

这时可以看到页面上的数据一直在增加，`useEffect()`被无限调用，进入无限循环状态。

# 🎉解决方法

这是一个错误使用`useEffect()`的常见问题。`useEffect()`可以看作是类组件中三个生命周期函数`componentDidMount`、`componentDidUpdate`和`componentWillUnmount`的组合。`useEffect(effect, deps)`接受两个参数:

*   `effect`副作用功能。
*   `deps`阵列的依赖性。

当`deps`阵列改变时，执行副作用功能`effect`。要修改方法，只需在`useEffect()`的第二个参数中传递`[]`:

```
export default function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    setCount(count + 1);
  }, []);
  return <div className="App">{count}</div>;
}
```

总结使用`useEffect`的四种情况:

*   **不要设置第二个参数**:当有状态更新时，会触发`useEffect`的副作用功能。

```
useEffect(() => {
  setCount(count + 1);
});
```

*   **第二个参数是空数组**:只有在挂载和卸载的时候才会触发`useEffect`的副作用函数。

```
useEffect(() => {
  setCount(count + 1);
}, []);
```

*   **第二个参数是一个单值数组**:只有值发生变化时才会触发`useEffect`的副作用函数。

```
useEffect(() => {
  setCount(count + 1);
}, [name]);
```

*   **第二个参数是一个多值数组**:只有当传递的值发生变化时才会触发`useEffect`的副作用函数。

```
useEffect(() => {
  setCount(count + 1);
}, [name, age]);
```

# 6.忘记清理使用效果中的副作用

# 🎀问题

在类组件中，我们使用`componentWillUnmount()`生命周期方法来清理一些副作用，比如定时器、事件监听器等。

# 🎉解决方法

可以为`useEffect()`的副作用函数设置返回函数，类似于`componentWillUnmount()`生命周期方法的作用:

```
useEffect(() => {
  *// Other Code*
  return () => clearInterval(id);
}, [name, age]);
```

# 📚证明文件

[React —使用钩子的例子](https://reactjs.org/docs/hooks-effect.html#example-using-hooks-1)

# 7.布尔运算符的使用不正确

# 🎀问题

在 JSX/TSX 语法中，我们经常使用布尔值来控制呈现的元素，并且在许多情况下我们使用`&&`操作符来处理这个逻辑:

```
const count = 0;
const Comp = () => count && <h1>Chris1993</h1>;
```

我们以为这个时候页面显示的是空的内容，实际上上面显示的是`0`的内容。

# 🎉解决方法

原因是因为 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 表达式导致`&&`之后的元素被跳过，但返回 falsy 表达式的值。所以我们尽量把判断条件写得尽可能完整，不依赖于 JavaScript 的布尔值的真假来比较:

```
const count = 0;
const Comp = () => count > 0 && <h1>Chris1993</h1>;
```

页面将显示空内容。

# 📚证明文件

[用逻辑& &运算符](https://reactjs.org/docs/conditional-rendering.html#inline-if-with-logical--operator)反应—内嵌 If

# 8.未定义组件参数类型

# 🎀问题

对于团队开发来说很常见。如果每个人开发的组件都没有定义好的参数类型，很容易让合作的同事不知道如何使用组件，非常麻烦，比如:

```
const UserInfo = (props) => {
  return (
    <div>
      {props.name} : {props.age}
    </div>
  );
};
```

# 🎉解决方法

解决方案是

*   使用 TypeScript，定义组件的`props`类型；

```
*// ClassComponent*
interface AppProps {
  value: string;
}
interface AppState {
  count: number;
}class App extends React.Component<AppProps, AppStore> {
  *// ...*
}*// FunctionComponent*
interface AppProps {
  value?: string;
}
const App: React.FC<AppProps> = ({ value = "", children }) => {
  *//...*
};
```

*   不使用 TypeScript，可以使用`propTypes`定义`props`类型；

```
const UserInfo = (props) => {
  return (
    <div>
      {props.name} : {props.age}
    </div>
  );
};UserInfo.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};
```

# 9.将字符串作为值传递给组件

# 🎀问题

由于 React 也有一个模板语法，与 HTML 非常相似，所以经常会出现数字作为道具直接传递给组件的情况，从而导致意外的值判断:

```
<MyComp count="99"></MyComp>
```

通过`MyComp`组件中的`props.count === 99`将返回`false`。

# 🎉解决方法

正确的方法应该是使用花括号来传递参数:

```
<MyComp count={99}></MyComp>
```

# 10.没有以大写字母开头的组件名称

# 🎀问题

刚刚起步的开发人员经常忘记以大写字母开始他们的组件名称。在 JSX/TSX 以小写字母开头的组件被编译成 HTML 元素，比如 HTML 标签的`<div />`。

```
class myComponent extends React.component {}
```

# 🎉解决方法

只需将第一个字母改为大写:

```
class MyComponent extends React.component {}
```

# 📚证明文件

[反应——渲染一个组件](https://reactjs.org/docs/components-and-props.html#rendering-a-component)

# 11.元素的事件绑定不正确

# 🎀问题

```
import { Component } from "react";export default class HelloComponent extends Component {
  constructor() {
    super();
    this.state = {
      name: "Chris1993",
    };
  } update() {
    this.setState({ name: "Hello Chris1993!" });
  }
  render() {
    return (
      <div>
        <button onClick={this.update}>update</button>
      </div>
    );
  }
}
```

点击`update`按钮时，控制台会报错:

```
Cannot read properties of undefined (reading 'setState')
```

# 🎉解决方法

这是因为`this`指出了问题所在，有几种解决方案:

*   在构造函数中绑定

```
constructor() {
  super();
  this.state = {
    name: "Chris1993"
  };
  this.update = this.update.bind(this);
}
```

*   使用箭头功能

```
update = () => {
  this.setState({ name: "Hello Chris1993!" });
};
```

*   在渲染函数中绑定(不推荐，每次组件渲染时创建一个新函数，影响性能)

```
<button onClick={this.update.bind(this)}>update</button>
```

*   在渲染函数中使用箭头函数(不推荐，每次组件渲染时创建一个新函数，影响性能)

```
<button onClick={() => this.update()}>update</button>
```

# 📚证明文件

如何将一个事件处理器(比如 onClick)传递给一个组件？

如果你觉得这篇文章不错，请点赞、评论、关注，你的支持是我分享的最大动力。😺

[](https://medium.com/@Chris1993/15-useful-custom-react-hooks-for-your-next-web-app-c5902d868f4c) [## 为你的下一个网络应用提供 15 个有用的自定义反应挂钩

### 本文与你分享 15 个非常有用的 React Hooks 函数。

medium.com](https://medium.com/@Chris1993/15-useful-custom-react-hooks-for-your-next-web-app-c5902d868f4c) [](/10-best-react-notification-libraries-in-2022-e06e8d338bb3) [## 2022 年 10 大最佳反应通知库

### 在这篇文章中，我将向你介绍一些伟大的第三方反应通知库，以帮助你成为一个…

javascript.plainenglish.io](/10-best-react-notification-libraries-in-2022-e06e8d338bb3) [](/how-to-develop-react-functional-components-with-typescript-12c2cfbb271d) [## 如何用 TypeScript 开发 React 功能组件

### 用 TypeScript 定义 React 功能组件的 4 种方法:使用 React。JSX 足球俱乐部。元素，反应。有孩子的建议，&…

javascript.plainenglish.io](/how-to-develop-react-functional-components-with-typescript-12c2cfbb271d) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***