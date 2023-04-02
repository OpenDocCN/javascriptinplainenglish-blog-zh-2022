# 如何在 React 中使用上下文 API

> 原文：<https://javascript.plainenglish.io/how-to-use-context-api-in-react-4d6293c9e032?source=collection_archive---------8----------------------->

![](img/5e21e8998682c53e7a51bcb3c2e6dd12.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**什么是语境？**
在外行人的术语中，语境的意思是“*某事发生或导致某事发生的情况*”。

**React 中上下文的重要性** 根据上面的定义，React 上下文将提供一个封装，在这个封装中，变量发生了变化，我们在相同的上下文中访问相同的变量。这里要注意的重要一点是，这种封装可以包含多个组件，因此有助于组件之间的变量共享或从顶部到底部组件的变量传播，反之亦然。

让我们尝试实现一个基本场景，以便更好地理解这一点。

**用例**

我们将实现一个基本的计数器应用程序。

![](img/f534ef0dc10b9ceec5cbb8f72615204f.png)

用户点击“增加计数器”按钮后，计数器值增加 1。

![](img/70c01e427a0bf8c0de997e37fddda2d2.png)

这里需要注意的重要一点是，显示值的按钮和标题在不同的组件中，我们在组件之间实时共享值。

让我们看看如何实现用例

*   首先，我们将做 react 应用程序的基础搭建

```
npx create react-app counter template=typescript
```

上述命令将创建一个基本的 React 应用程序。

接下来，我们将创建两个基本组件。

**割台组件**

```
// Header.tsx

const Header = () => {
    return(
        <h1>Counter value is </h1>
    )
}

export default Header;
```

**车身部件**

```
 // Body.tsx

const Body = () => {
    const incCounter = () => {

    }
    return(
        <button onClick={incCounter}>
            Increase Counter
        </button>
    )
}

export default Body
```

**更新 App.tsx** ,删除返回块中的所有代码

```
// App.tsx

return (
    <>
      <Header/>
      <Body/>
    </>
  );
```

我们已经有了基本的结构，现在我们将深入实现上下文。

1.  创建一个名为 CounterContext.tsx 的文件，并添加以下代码

```
import { createContext, useState } from "react";

// Step 1
const CounterContext = createContext({
counter : 0,
handleCounter : () => {}
});

// Step 2
const CounterProvider = ({children}:{children:any}) => {
// Step 3
const [counter,setCounter] = useState(0);
//Step 4
const handleCounter = () => {
setCounter((prevValue:any) => prevValue + 1);
}
//Step 5
const counterObj = {counter,handleCounter}
// Step 6
return(
<CounterContext.Provider value={counterObj}>
{children}
</CounterContext.Provider>
)
}
// Step 7
export { CounterProvider , CounterContext}
```

不要被这么多行代码吓倒，因为这是上下文的基本要点，我们将一步一步地检查每一行。

1.  在**步骤 1** 中，我们使用名为反上下文的 **createContext** 创建了上下文。createContext 是 react 提供的一种方法，它有助于创建一个上下文，其中所有组件都封装在需要访问或共享变量的地方。这里要注意的另一件事是，createContext 应该公开我们需要在封装组件中访问的变量和方法，例如，在我们的示例中，counter 变量和 handleCounter 方法被公开。
2.  在步骤 1 中创建的上下文有一个提供者反应组件。使用这个提供者的优点是，它提供了一个包装器，我们可以在其中包装所有想要订阅上下文更改的组件。在**步骤 2** 中，我们创建了一个名为 **CounterProvider** 的函数，它返回一个 react Provider 组件。
3.  在**步骤 3** 中，我们简单地创建了一个计数器变量，并使用 setCounter 为其创建了 useState 钩子和 setter。
4.  在**步骤 4** 中，我们创建了 handleCounter 方法，该方法将触发计数器变量的 setter。
5.  **第 5 步**是真正的业务，在这里我们定义了属性、方法，我们需要将这些属性、方法公开给我们包装了 Provider 的组件。请注意，步骤 1 中定义的对象结构应该与此处定义的对象结构匹配，否则将出现类型不匹配错误。您可以将步骤 1 中定义的结构视为别名，将步骤 5 中定义的结构视为真正的实现。
6.  在步骤 2 中返回的提供程序反应组件需要一个 value provider，我们在其中传递了在步骤 5 中定义的对象，这样就可以在封闭组件中使用该对象。
7.  最后，在**步骤 7** 中，我们导出了这样创建的上下文和提供者，可以在外部访问它们。

通过上面提到的步骤，我们已经完成了 CounterContext 的实现，在大多数情况下，这是所需的 7 个基本步骤，棘手的用例和复杂性可能会有所不同。

现在，让我们使用这个创建的上下文来实现我们的用例。

*   一旦我们准备好 CounterProvider 组件，我们将在 App.tsx 中使用它，并如下所示将其包装在 Header 和 Body 组件周围。我们将围绕我们希望在其中访问上下文的组件包装提供程序。

```
 return (
    <CounterProvider>
      <Header/>
      <Body/>
    </CounterProvider>
  );
```

让我们更改 Body 组件以触发计数器变量的更改。

*   车身部件

```
import { useContext } from "react";
import { CounterContext} from './CounterContext';

const Body = () => {

const { handleCounter} = useContext(CounterContext); // Step 1
const incCounter = () => {       // Step 2
handleCounter();
}
return(
<button onClick={incCounter}>
Increase Counter
</button>
)
}

export default Body
```

1.  在**步骤 1** 中，我们使用的是由 reactor 提供的 useContext api。它接受一个参数，即上下文的名称。传入上下文名称后，它将返回在 value prop 中传递的对象或属性，同时返回 Provider 组件。在我们的例子中，它会像——

```
 <CounterContext.Provider value={counterObj}>
            {children}
        </CounterContext.Provider>
```

我们使用析构获得 handleCounter 属性。

2.在**步骤 2** 中，我们通过点击按钮调用 handleCounter。如果您还记得 handleCounter 方法是我们在中使用 setCounter 设置新的计数器值的方法。因此，在单击 Button 时，上下文中的计数器变量将被更新。

现在，让我们在 header 组件中进行更改，以订阅对 counter 变量所做的更改

*   表头组件

一旦生产者更新了这个值，我们就需要在其他组件中使用相同的值。让我们对 Header 组件进行一些更改。

```
import { useContext } from "react";
import { CounterContext } from "./CounterContext";
const Header = () => {
const { counter } = useContext(CounterContext);   // Step 1 
return(
<h1>Counter value is - {counter}</h1>           // Step 2 
)
}
export default Header;
```

1.  在**第 1 步**中，我们再次使用了 useContext api，这一次我们得到了一个计数器变量，它是点击 Body 组件中的按钮后的更新值。
2.  在**步骤 2** 中，我们显示计数器变量。

这就是我们如何使用 Context 和 useContext api 在 reaction 中将值从一个组件传递给另一个组件。

你可以在[回购](https://github.com/Avinash219/Context_Tutorial)找到完整的代码片段。

如果你有任何进一步的疑问，请及时和我联系。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript 和 UI/UX 相关的东西。点击[这里](https://medium.com/@avinash.dev21987)阅读我所有的文章，并让我知道你的反馈。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****