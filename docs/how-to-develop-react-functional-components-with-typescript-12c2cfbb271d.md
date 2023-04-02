# 如何在 TypeScript 中使用 React 功能组件

> 原文：<https://javascript.plainenglish.io/how-to-develop-react-functional-components-with-typescript-12c2cfbb271d?source=collection_archive---------0----------------------->

## 用 TypeScript 定义 React 功能组件的 4 种方法。

![](img/abcd0f071309ff9b384ebab94a545398.png)

photo via [https://pixabay.com/](https://pixabay.com/)

当我们使用 React 开发项目时，使用最多的应该是组件，组件分为**功能组件**和**类组件**，我们可以定义如下:

*   定义功能组件

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

*   定义类组件

```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

在本文中，我将介绍使用 TypeScript 定义功能组件的 4 种方法，以及在使用过程中需要注意的几个问题。

[如何用 TypeScript](#43cb) 定义功能组件
∘ [⭐ 1。使用 React。FC](#0b21)
∘ [⭐ 2。利用 JSX。元素](#f922)
∘ [⭐ 3。直接定义完整类型](#380d)
∘ [⭐ 4。使用 React。props withschildren](#9502)
[温馨提示](#4383)
∘ [🎉 1.功能组件不能返回布尔值](#ac29)
∘ [🎉 2.无法使用 Array.fill()填充组件](#f14c)
∘ [🎉 3.支持通用组件](#db25)
[引用](#e5ea)

# 如何用 TypeScript 定义功能组件

功能组件通常接受一个`props`参数并返回一个 JSX 元素或`null`。

当我们需要使用 TypeScript 来定义一个功能组件的时候，我们有 4 种方式，每种方式都有自己的优缺点，具体情况而定。

## ⭐ 1.使用 React。足球俱乐部

由于 React 不是用 TypeScript 开发的，它使用社区开发的`@type/react`包提供的类型，该包有一个通用类型`FC`，允许我们向功能组件添加类型。

```
type FCProps = { text: string };const FCComponent: React.FC<FCProps> = ({ text = "" }) => <div>{text}</div>;
```

这里的`React.FC`是`React.FunctionComponent`的简写。

当组件包含子元素时，TypeScript 将提示警告:

Using React.FC

提示警告内容:

```
Type '{ children: string; text: string; }' is not assignable to type 'IntrinsicAttributes & FCProps'.
  Property 'children' does not exist on type 'IntrinsicAttributes & FCProps'.
```

这现在已被否决。有关具体讨论，请参见以下两个链接:

*   [清除 React。来自类型脚本模板#8177](https://github.com/facebook/create-react-app/pull/8177) 的 FC；
*   [TypeScript + React:我为什么不用 React。T42 舰队指挥官.](https://fettblog.eu/typescript-react-why-i-dont-use-react-fc/)

## ⭐ 2.利用 JSX。元素

使用`JSX.Element`类型作为功能组件的返回值类型。当组件的返回值不是`JSX.Element`类型时，TypeScript 会提示错误。

Using JSX.Element

## ⭐ 3.直接定义完整类型

由于`React`组件包含一个子元素，它会隐式传递一个`children`属性，导致定义的参数类型出错，所以我们可以直接定义一个完整的参数接口，包括`children`属性的类型:

Define the full type directly

## ⭐ 4.使用 React。有孩子的建议

第三种方法更麻烦，每次手工编写一个`children`属性类型，那么我们可以使用`React.PropsWithChildren`类型，它本身封装了`children`类型声明:

```
*// react/index.d.ts*
type PropsWithChildren<P> = P & { children?: ReactNode };
```

因此，使用`React.PropsWithChildren`类型来定义功能组件，而不必处理`children`的类型:

Using React.PropsWithChildren

# 技巧

## 🎉 1.功能组件不能返回布尔值

当我们在函数组件中使用条件语句时，如果 React 返回非 JSX 元素或非空值，它将抛出错误:

Functional Components cannot return boolean values

正确的做法是让功能组件返回有效的 JSX 元素或 null:

当然，你不能这样写，当属性`useRender`是`false`时，它也会出错:

```
const ConditionComponent = ({ useRender = false }) =>
  useRender && <span>Render ConditionComponent</span>;*// ❌*
```

## 🎉 2.无法使用 Array.fill()填充组件

当我们的组件直接返回`Array.fill()`的结果时，TypeScript 抛出错误。

Unable to use Array.fill() to fill components

提示以下内容:

```
'ArrayComponent' cannot be used as a JSX component.
  Its return type 'any[]' is not a valid JSX element.
    Type 'any[]' is missing the following properties from type 'ReactElement<any, any>': type, props, key
```

为了解决这个问题，我们可以定义函数的返回类型:

```
const ArrayComponent = () =>
  Array(3).fill(<span>Chris1993</span>) as any as JSX.Element; *// ✅*
```

## 🎉 3.支持通用组件

在使用 TypeScript 开发 React 功能组件时，还可以使用泛型来约束和声明泛型组件，这样可以使我们的组件更加灵活。

它可以这样使用:

Support Generic Components

更高级的用法在[通用组件](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase#generic-components)章节中描述:

[Generic Components](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase#generic-components)

# 参考

*   [反应](https://reactjs.org/)
*   [React 打字稿备忘单](https://react-typescript-cheatsheet.netlify.app/)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***