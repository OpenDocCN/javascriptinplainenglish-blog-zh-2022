# React Hooks:终极指南(useRef)

> 原文：<https://javascript.plainenglish.io/react-hooks-the-ultimate-guide-useref-c89fd26574b2?source=collection_archive---------9----------------------->

![](img/a4524c44ba66fe986aa1550386bef870.png)

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

访问 DOM 元素有时很麻烦，但是自从 react 钩子出现以来，我们有了一种简单的方法。`[useRef](https://reactjs.org/docs/hooks-reference.html#useref)`有不同的用例，但最常用的是轻松访问元素的 DOM。

但是首先…

## 什么是`useRef?`

> `useRef`返回一个可变的 ref 对象，其`.current`属性被初始化为传递的参数(`initialValue`)。返回的对象将在组件的整个生存期内保持不变。

`useRef`作为一个函数工作，它将返回给我们一个 [ref](https://pt-br.reactjs.org/docs/refs-and-the-dom.html) 对象，并将接收一个值，该值将是这个 ref 的初始值。ref 中的属性`current`将发送初始值。

## 什么时候用？

相应地，在 React 的文档中，有三个很好的`useRef`用例

*   管理焦点、文本选择或媒体播放。
*   触发命令式动画。
*   与第三方 DOM 库集成。

我想再补充两点:

*   用于保存一个可变变量，但我们不希望它在 DOM 中被更新以供用户查看。
*   另一个场景是保存状态的先前值

## 访问 DOM

假设我们有一个输入，我们希望这个输入集中在一个按钮的点击上。我们可以这样做:

在这段代码中，我们使用`useRef.current.focus`来访问通过 ref 传递的输入的`focus`。

## 保持可变变量

可变变量意味着我们希望能够更新变量的值。但是假设我们不想在屏幕中更新这个值。在这种情况下，我们可以这样做:

在这段代码中，我们在每次输入改变时更新`ref`,但是当它发生时，屏幕上不会显示出来(正如我们在控制台中看到的，它在`ref`的值中被更新)。一旦我们单击该按钮，该值将被发送到`useState`，它将为我们显示该值，即使“useRef Value”仍然为空。

## 访问以前的值

现在为了表示这个例子，让我们假设我们想要创建一个组件，当用户点击一个按钮时，我们给一个计数器值加 1，但是我们也想要保存旧的值。

在这个例子中，每次我们改变`useState`值，都会触发重新渲染和`useEffect`。这样，我们可以将旧值保存在 ref 中，将实际值保存在`useState`中。

嗯，这涵盖了我倾向于使用`useRef`的大多数用例，我希望这能帮助你更好地理解它。

干杯！

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*