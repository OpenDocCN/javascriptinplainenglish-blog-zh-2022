# React 的另一个状态管理库:Zustand

> 原文：<https://javascript.plainenglish.io/another-state-management-library-for-react-zustand-3eecdcec274b?source=collection_archive---------8----------------------->

## Redux 和 hooks 的最佳之处，样板文件最少

![](img/e1e31d0bbcb13f6c30915ef41453d406.png)

The official banner

自从 React 存在以来，我们已经看到了很多用于 React 的**状态管理库**。从 **Redux** 到 **Context** ，还有**反冲**(那已经实验了快 3 年了)。

然而，我今天发现了一个新的版本，它允许**很少的样板文件**，但是却有一个**愉快的体验** : **Zustand** 。

[](https://www.npmjs.com/package/zustand) [## 祖斯坦德

### 一个小型、快速和可扩展的 bearbones 状态管理解决方案，使用简化的 flux 原理。基于舒适的 api

www.npmjs.com](https://www.npmjs.com/package/zustand) 

Zustand 使用钩子的力量来管理我们的状态。它的强大之处在于不需要用上下文或其他提供者来包装你的组件。相反，你所要做的就是创建你自己的钩子，并直接定义它里面的状态和设置器。

使用 **Zustand** 的伟大之处在于，如果你没有使用的值在存储区内发生变化**(不同于上下文)**，它**不会触发组件的重新渲染**

## 让我们开始吧

使用您最喜欢的应用程序引导程序(在我的例子中，我将使用 **Vite** ，创建一个新的应用程序，并在您的代码编辑器中打开它。

我们要做的第一件事是创建一个新的**文件，在其中声明我们的商店**。我们将创建一个简单的存储，其中包含一个计数器和一个增量操作。

```
import create from 'zustand';

const useCounterStore = create((set) => ({
  count: 0,
  actions: {
    increment: () => set((state) => ({count2: state.count2 + 1})),
  }
}))
```

这是多么的简单，令人难以置信。我们店现在已经可以用了，没有必要再做什么了！！

现在，为了遵循一些好的实践，我们将创建特殊的挂钩来获取计数器值或操作

```
 export const useCounter = () => useCounterStore((state) => ({count: state.count}))

export const useCounterActions = () => useCounterStore(state => state.actions)
```

我们现在准备在我们的组件中使用钩子，让奇迹发生！

```
function App() {
  const {count} = useCounter();
  const {increment} = useCounterActions();

  return (
    <div className="App">
      counter {count}
      <button onClick={increment}>Increment</button>
    </div>
  )
}
```

就这么简单！请随意调整和使用它，因为这是一篇非常小的介绍性文章。

如果你想知道更多和更深入的阅读，请随意阅读创作者的这篇精彩文章:

[](https://tkdodo.eu/blog/working-with-zustand) [## 使用 Zustand

### 全局(客户端)状态管理并不总是像今天这样。我清楚地记得我们最好的选择是…

tkdodo.eu](https://tkdodo.eu/blog/working-with-zustand) 

我希望你喜欢这篇文章，并希望你能发现一个伟大的新的 React 状态管理解决方案！我可能会在我当前的项目中自己使用它，因为它们是上下文的一个很好的替代品，并且减少了许多样板文件！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***