# React Fragment vs: Why You Should Use the Former

> 原文：<https://javascript.plainenglish.io/react-fragment-vs-div-d4d1b3090981?source=collection_archive---------2----------------------->

## 向 React 组件添加多个元素的一种更现代、更好的方式，无需将它们包装在额外的 DOM 节点中

当我开始学习 React 时，我经常在返回之前使用

作为父元素或包装器来包装多个元素，但这将导致 DOM 树的大小不必要地增加，所以当我发现 React 片段时，就像一样，但不会增加 DOM 树，我欣喜若狂。![](img/2945269d334a3d34d5ac77ccd22738ba.png)

## **使用<div>**

```
<div>
   Hello world
</div>
```

一个

元素具有原型链 HTMLDivElement = > html Element = > Element = > Node = > event target，而一个文档片段具有 document fragment = > Node = > event target。这意味着有更多的方法和属性，这会导致大量的内存使用。

每当我们想从 return 语句中返回多个元素时，我们使用一个

来包装内容，我们就创建了一个额外的节点，这个额外的 div 可能会在 HTML 中析构 DOM。

## **使用<div>T8 的问题】**

*   增加 HTML DOM 的大小。结果，用户的浏览器消耗额外的能量来在浏览器上处理你的网站。
*   过大的 DOM 会导致高内存使用率、样式处理滞后和页面加载时间变慢。
*   在旧设备上，这会导致 HTML 混乱，从而导致性能问题。
*   由于更大、嵌套更多的 DOM，调试和跟踪额外节点的来源变得更具挑战性。
*   使用 Flexbox 和 Grid 很难维护所需的布局，因为它们具有唯一的父子关系，添加 div 会破坏标记。

## **使用<做出反应。片段>**

```
<React.Fragment>
   Hello world
</React.Fragment>
```

或者，您甚至可以使用如下所示的短语法:

```
<>
   Hello world
</>
```

React 片段是向 React 组件添加多个元素的一种更现代、更好的方式，无需将它们包装在额外的 DOM 节点中，如

等。

这消除了包装器

,包装器会导致无效的 HTML 和上面提到的许多其他问题。

## **使用< React 的优点。片段>**

*   更好的代码可读性。
*   增加了 JSX 以前没有的功能。
*   更好的语义 JSX 标记。像这样的包装元素在需要的时候使用，不是因为你被迫返回一个包装元素。
*   较少的 dom 标记会提高渲染性能并减少内存开销。

![](img/02fa458ff0769220f5531154ef22bd99.png)

## **结论**

React 片段在某些场景下比

标签更好。知道什么时候用 **< div >** 和什么时候用< **反应。片段>** 是每个 react 开发者都应该知道的重要技能。它们并不是在所有情况下都可以互换，但是在你被迫使用< div >的情况下，尤其是在返回多个元素的时候，React 片段绝对是一个很好的选择。你不仅能写出更干净、可读性更强的代码，还能占用更少的内存，更快地渲染组件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*