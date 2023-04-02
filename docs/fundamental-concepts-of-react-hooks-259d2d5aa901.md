# 理解 React 钩子的基本概念

> 原文：<https://javascript.plainenglish.io/fundamental-concepts-of-react-hooks-259d2d5aa901?source=collection_archive---------12----------------------->

React 16.8 引入了一种叫做钩子的新模式，使用功能组件来处理状态和其他 React 特性。在 React 版之前，开发人员只能使用类组件来处理状态和生命周期。

![](img/764af090f13168f36f5d1aeff294da77.png)

> *钩子让你一直使用函数，而不是在函数、类、hoc、渲染道具之间切换。*

开始使用 React 钩子的最好方法是学习如何使用它们。在这篇文章中，我将分享“在使用钩子时你应该做什么和不应该做什么”，以避免任何含糊不清。最后，我补充了几点来帮助你理解 Hook 在第三方库中的支持。

# **1。遵循挂钩规则**

> **总是在 React 函数的顶层使用钩子**

1.  不要在循环、条件或嵌套函数中调用钩子。

2.在任何提前返回之前，总是使用钩子。

3.钩子在每次渲染时都以同样的顺序被调用。

通过遵循这条规则，您可以确保每次组件呈现时都以相同的顺序调用钩子。这允许 React 正确地保存多个`useState`和`useEffect`调用之间的钩子状态。

> 不要从常规的 JavaScript 函数中调用钩子。

相反:

1.您可以从 React 函数组件调用挂钩

2.您可以从自定义挂钩中调用挂钩

# 2.自定义**挂钩名称必须以“** `**use"**` **开头，后跟一个大写字母**

像 useState(内置)或 useUserStatus，这是非常重要的。没有它，React 就不能自动检查对 Hook 规则的违反

# **3。使用名为 eslint-plugin-react-hooks 的 ESLint 插件来执行钩子的**规则

要在您的项目中设置它，请遵循以下说明

假设您已经安装了 ESLint，运行:

```
# npm
npm install eslint-plugin-react-hooks --save-dev# yarn
yarn add eslint-plugin-react-hooks --dev
```

然后扩展推荐的 eslint 配置:

```
{
  "extends": [
    // ...
    "plugin:react-hooks/recommended"
  ]
}
```

对于自定义/高级配置，请遵循此处提到的详细信息[**eslint-plugin-react-hooks**](https://www.npmjs.com/package/eslint-plugin-react-hooks)

*注:该插件默认包含在*[*Create React App*](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app)*中。*

# 4.你不能在类组件中使用钩子*，*

但是你绝对可以在同一个项目中用钩子混合类和函数组件。

# 5.自定义挂钩中的状态和效果是完全隔离的

使用同一个钩子的两个组件不能共享状态和效果。但是你可以在钩子之间传递信息。

## 如果你已经走了这么远，非常感谢你阅读我的帖子，这里有一些奖励点给你

1.  与 componentDidMount、componentDidUpdate、componentWillUnmount 相关的用例可以由 [useEffect 挂钩](https://reactjs.org/docs/hooks-reference.html#useeffect)覆盖

2.还没有钩子来覆盖 getSnapshotBeforeUpdate、getDerivedStateFromError 和 componentDidCatch 生命周期。

3.从 7.1.0 版开始，React Redux 中增加了钩子支持

4.React 路由器[从 v5.1 开始支持钩子](https://reacttraining.com/react-router/web/api/Hooks)

我希望这篇文章能帮助你学习 React 钩子的规则以及如何正确使用它们。如果你喜欢这篇文章，请使用👏按钮。关注我，获取更多关于 React、React Native、JavaScript 和软件开发的文章。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。****