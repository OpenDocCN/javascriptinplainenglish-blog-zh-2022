# 回应面试问题— MCQs

> 原文：<https://javascript.plainenglish.io/react-interview-questions-mcqs-69be6132af33?source=collection_archive---------1----------------------->

## 技术能力倾向测验中常见选择题列表。

![](img/f2c256edab15053f129436f5355d87f7.png)

Photo by [Nguyen Dang Hoang Nhu](https://unsplash.com/@nguyendhn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个**开源 JavaScript 库**，主要用于设计和开发**可重用组件**。具有 JavaScript 背景的开发人员可以很容易地学习 React 并动手操作。React 是 web 开发人员和组织正在使用的最流行的前端技术。如果你正在准备 React 面试，下面是你必须知道的问题列表。

下面列出了在不同平台上最常被问到的 React 问题，这些问题用于进行第一轮筛选。

**1。React 使用真实的 DOM 吗？**

A.真
B .假

**2。以下哪一项不是 React 生命周期方法？**

A.`static getDerivedStateFromProps()`
b .`shouldComponentUpdate()`
c .`getSnapshotBeforeUpdate()`
d .`gethandleChange()`

**3。纯组件内部使用哪种生命周期方法？**

A.`shouldComponentUpdate()`
b . `getSnapshotBeforeUpdate()`
c .`static getDerivedStateFromProps()`
d .`componentDidMount()`

**4。React 钩子是在哪个 React 版本中引入的？**

A.16.2
b . 16.4
c . 16.6
d . 16.8

**5。借助钩子，无需编写类就可以使用状态和反应生命周期。**

A.真
B .假

**6。useState 钩子的返回值是什么？**

A.当前状态
B .函数更新当前状态
C .当前状态和函数更新当前状态的配对
D. UseState 返回 nothing

为了方便起见，我在这里给出了前 6 个选择题的答案:

![](img/689ae80dd453683667f61f6cb15e34f1.png)

Photo by [Michal Matlon](https://unsplash.com/@michalmatlon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

1.  **B**
    React 内部使用虚拟 DOM。它是真实 DOM 的内存虚拟表示。计算当前和先前虚拟 DOM 表示之间的差异，并且将唯一的差异更新到真实 DOM，这有助于增强应用程序的性能。
2.  **D**
    `gethandleChange()`不是 React 生命周期方法。下面是 React 生命周期方法的列表:

    1。`static getDerivedStateFromProps()` 2。`render()` 3。`componentDidMount()` 4。`static getDerivedStateFromProps()`
    5。`shouldComponentUpdate()`
    6。`getSnapshotBeforeUpdate()`
    7。`componentDidUpdate()`
    8。`componentWillUnmount()`
3.  **A**T24`shouldComponentUpdate()`方法由纯组件在内部处理。说明:根据应用程序的状态或道具是否改变，纯组件确定是否重新渲染。它通过在内部处理前一个和下一个状态的浅层比较来提高性能。
4.  **D**16.8
    说明:16.8 版本增加了 React 钩子。通过使用 React 钩子，我们可以在功能组件中拥有状态和生命周期方法。在 16.8 版之前，我们无法在功能组件中使用状态和生命周期方法。为此，我们必须使用类组件。
5.  **一**一
    真
6.  **C**
    对当前状态和功能进行更新。
    解释:我们可以使用`useState()`钩子在函数组件内部设置状态。`useState()`接受初始状态值作为默认值，并返回当前状态和更新当前状态的方法。

现在，我将继续回答其余的问题。

![](img/7869a7043d6c5e291cf8d9f4c232f585.png)

Photo by [Remi Turcotte](https://unsplash.com/@turkomarketing?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**7。哪种说法更适合下面的代码片段？**

```
useEffect(() => {
         //Code logic 
        }, [TnS_user]);
```

A.效果仅在挂载
时运行 b .如果 TnS _ 用户值为真
效果重新运行 c .当且仅当 TnS _ 用户变量的值发生变化
D .以上所有

**8。以下哪一项不是网格断点？**

A.xs
B. sm
C. md
D. xd

**9。在 React 中，组件名应该总是以大写字母开头，因为 React 将以小写字母开头的组件视为 DOM 标签。**

A.真
B .假

**10。关于** `**React.lazy**` **，以下哪一项是正确的？**

A.它有助于大数据的动态渲染。
B .用于处理异步函数。c .它将动态导入作为常规组件呈现。
D .它限制组件重新渲染。

**11。以下哪种方法用于在 React 错误边界中呈现回退 UI？**

A.`static getDerivedStateFromProps()`
b .`static getDerivedStateFromError()`
c .`componentWillCatch()`
d .`shouldComponentCatch()`

**12。错误边界不会捕捉以下哪种错误？**

A.`setTimeout()`
B .事件处理程序
C .服务器端渲染
D .以上全部

**13。在 React 中，我们可以通过使用？**

A.`preventDefault()`
b .`DefaultPrevent()`
c .`stopDefault()`
D . A 和 D

14。Comp1、Comp2 和 Comp3 是三个 react 组件。考虑到在父组件的渲染中调用了以下代码片段，哪一个是正确的？

```
1\. return (
    <div>
      <Comp1/>
      <Comp2/>
      <Comp3/>
    </div>
  );

2\. return (
      <Comp1/>
      <Comp2/>
      <Comp3/>
  );3\. return (
    <React.Fragment>
      <Comp1/>
      <Comp2/>
      <Comp3/>
    </React.Fragment>
  );4\. return (
    <React.Fragment>
      <Comp1/>
      <Comp2/>
    </React.Fragment>
    <Comp3/>
  );5\. return (
   <div>
      <div>
         <Comp1/>
         <Comp2/>
      </div>
         <Comp3/>
   </div>
  );
```

A.1，2，5
B. 1，3，5
C. 2，3，5
D. 4，5

以下是问题 7-12 的答案列表。请检查上述问题 1-6 的答案。

![](img/7aa3ccdb811271cf952095f5e30b3110.png)

Photo by [Akhilesh Sharma](https://unsplash.com/@fotonium?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

7.当且仅当 TnS _ 用户变量的值改变时，效果才重新运行。
解释:问题中给出的代码片段具有 useEffect 钩子，其功能类似于`shouldComponentUpdate()`方法。作为第二个参数传递给`useEffect()`的数组可以是空的**或者可能有一些状态变量。
如果数组为空，它将像`**componentDidMount()**`一样运行，并且在渲染组件时只被调用一次。根据给定的例子，如果它有任何状态变量，它将只在**状态变量的值更新**时被调用。**

8. **D**
下面是网格断点及其分辨率的列表。
1。sm —用于屏幕分辨率 **≥ 576px** 的小屏幕设备。
2。md —适用于屏幕分辨率 **≥ 768px** 的平板设备。
3。lg —适用于屏幕分辨率 **≥ 992px** 的笔记本电脑等较大设备。
4。xl —用于超大设备，如屏幕分辨率 **≥1200px** 的台式机。

9.A
真
解释:在 React 中我们用 JSX。在 JSX，所有小写标签都被认为是 HTML 标签。因此，为了避免这种冲突，react 组件名称应该以大写字母开头。

10. **C**
它将动态导入渲染为常规组件。
解释:`React.lazy`函数让您将动态导入渲染为常规组件。

```
//Without React.lazy()
import LazyComponent from './LazyComponent';//with React.lazy()
const LazyComponent = React.lazy(() => import('./LazyComponent'));
```

当这个组件第一次被渲染时，它将自动加载包含`LazyComponent. React.lazy`的包，这个包采用一个必须调用动态`import()`的函数。这必须返回一个`Promise`，它解析为一个带有包含 React 组件的`default`导出的模块。

11. **B** 早先在 JavaScript 中没有办法处理这个问题，但是 react 在 v-16 中提供了错误边界。
错误边界不过是 react 组件，它将捕捉任何子组件中的错误，记录该错误，并显示回退 UI，而不是显示空白的崩溃页面，该 UI 将向用户提供一些有意义的消息，而不是显示崩溃的应用程序。
错误边界不捕捉`setTimeout()`的错误、事件处理程序以及错误边界本身发生的错误。

12. **D**

13. **A**
`preventDefault()`
解释:为了防止事件处理程序的默认行为，我们可以使用 **event.preventDefault()** 。它将阻止浏览器发出默认行为。

14.**B
1，3，5
说明:React render 应该总是返回单个对象。我们可以有嵌套的封闭标签，这些标签必须被一个父标签所封闭。在选项 3 中，我们有 React **片段**，这些片段**没有向 DOM 添加额外的节点**，因此被认为比 div 更好。**

这是我碰到的 React 的几个选择题的列表。我试图根据我的理解和知识来解释。就这样，我们到了这篇文章的结尾。如果你觉得这篇文章有帮助，请不要忘记检查其他文章！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***