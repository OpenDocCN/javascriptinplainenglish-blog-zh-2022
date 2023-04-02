# 如何使用条件渲染在 React 中创建切换按钮？

> 原文：<https://javascript.plainenglish.io/how-to-do-conditional-rendering-in-react-and-create-a-toggle-button-4a0e3b5565ed?source=collection_archive---------4----------------------->

## 使用 useState 挂钩创建一个切换按钮来显示和隐藏数据。

在 React 中，有几种方法可以有条件地呈现某些内容。您可以使用&&运算符或条件呈现来显示和隐藏 JSX 中的数据。

## 如果使用逻辑&运算符

你会看到苹果写在你的本地主机上。那么它是如何工作的呢？

首先，我们创建了一个布尔变量 apple，并赋予它一个*‘true’*值。我们可以在 JSX 中访问这个变量，在花括号内，我们可以放入条件逻辑。

```
<div>{**apple && <h2>Apple</h2>**}</div>
```

这里苹果是变量，我们的 h2 标签只有在苹果为真时才有效，如果苹果不再为真(变为假)，h2 标签就不起作用了，因为我们的条件颠倒了(假)。

`true && expression`总是评估为`expression`，`false && expression`总是评估为`false`。

为什么不试着把苹果的值改成 false，看看会发生什么？

## 带有条件运算符的 If-Else

JavaScript 条件操作符`[condition ? true : false](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)`在 JSX 内部也能工作。

```
<div>**{apple ? "Apple" : "Banana"}**</div>;
```

如果苹果为真，则输出苹果，否则输出香蕉。

# React 中的切换按钮

在 React 中，为了管理本地状态，我们必须使用功能组件内部的钩子。你不能像这样简单地更新你的状态:

```
 const handleChange=()=>{
     return !changeText
}
```

您必须通过 useState 钩子更新状态，并在顶层导入它。

```
let [changeText, setChangeText] = useState(true);
```

括号中的文本被赋值给某个值，称为数组析构。

```
const foo = ['one', 'two', 'three'];

const [red, yellow, green] = foo;
console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"
```

你可以在按钮上添加一个 onClick 回调函数，这样当你点击按钮的时候，它就会调用 handleChange 函数，这个函数会把 changeText 的布尔值从 true 改为 false。

就这样，现在你有了一个可重用的切换组件，可以在你的应用程序中使用了。

> **关注我的 YouTube 频道获取更多编码教程:**[**https://www.youtube.com/channel/UCOHJCOprtOf4caI50lJlHSQ**](https://www.youtube.com/channel/UCOHJCOprtOf4caI50lJlHSQ)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*