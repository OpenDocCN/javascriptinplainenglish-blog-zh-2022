# React 中 useState 和 useRef 的区别

> 原文：<https://javascript.plainenglish.io/the-difference-between-usestate-and-useref-in-react-fa3ccd9aeda5?source=collection_archive---------0----------------------->

## React 中的 useState vs useRef:你需要知道的一切。

![](img/038d0b64e4db12e170c2ff925650a88e.png)

Photo by [Jannis Brandt](https://unsplash.com/@jannisbrandt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个非常流行的用于构建用户界面的 JavaScript 库。很多开发人员更喜欢这个库，因为它完全基于组件，并且有很多我们可以使用的很酷的包。除此之外，现在我们有了 React 钩子，它把我们从复杂的类组件中解救了出来。

React 钩子非常强大，允许我们在功能组件中使用状态。它们还让我们能够在无状态功能组件中创建逻辑和功能。许多开发人员现在更喜欢使用钩子和功能组件，而不是类组件，因为类语法有点难写。您可以在 React 代码中使用许多有用的挂钩来创建逻辑并向组件添加特性。

这就是为什么在本文中，我们将通过介绍钩子 useState 和 useRef 之间的区别来了解它们。所以让我们开始吧。

# useState 挂钩

挂钩 useState 只是一个接受一个参数(初始状态)并返回两件事的函数:

当前状态(我们状态的值)。允许我们更新当前状态功能。钩子 useState 允许我们在功能组件中拥有状态，我们可以用它在 React 中创建许多很酷的东西。例如，使用 useState，我们可以在单击按钮后更改文本，或者创建计数器等等。在 React 中，您可以使用这个重要的钩子做很多事情。

所以如果你想在 react 中使用 useState，你必须首先从 React 包中导入它。

这里有一个例子:

```
import React, { useState } from 'react'
```

现在，从 react 包中导入它之后，您就可以在功能组件中使用钩子了，不会有任何问题。

# 例子

在下面的例子中，我们将使用钩子 useState 来创建文本，并在单击按钮后更新它:

```
//import useState.
import React, { useState } from 'react'function MyComponent() {
    // Using useState.
  const [name, setName] = useState('Mehdi') //JSX.
  return(
      <>
      <h1>{name}</h1>
      <button onClick={()=> setName("John")}>Change Name</button>
      </>
  )
}export default MyComponent;
```

正如你在上面看到的，钩子 useState 允许我们在点击按钮后更新状态。我们传递了一个字符串名作为钩子函数的参数，你可以传递任何东西，比如数组，数字，布尔值，所有这些都取决于你处理的是什么类型的状态。

另外，请注意，我们使用 ES6 数组析构来指定初始状态和更新函数。值名指的是初始状态“Mehdi ”,值集名指的是允许 up 更新状态的函数。我们还在 click 事件中调用了更新函数 setName，以便将名称状态从“Mehdi”更新为“John”。因此，单击按钮后，标题 h1 内的值名称会得到更新。

所以钩子 useState 非常有用，因为它允许我们在函数组件中使用状态并更新它，而不必使用类语法。

下面是另一个计数器的例子，它允许我们在单击一个按钮后将数字增加 1:

```
//import useState.
import React, { useState } from 'react'function MyComponent() {
    // Using useState.
  const [counter, setCounter] = useState(0) //JSX.
  return(
      <>
      <h1>{counter}</h1>
      <button onClick={()=> setCounter(counter + 1)}>Increment</button>
      </>
  )
}export default MyComponent;
```

在这个例子中，我们将初始状态设置为 0，作为钩子函数的参数。这是因为我们在处理数字，我们需要在每次点击按钮时将数字加 1。更新函数 setCounter 允许我们将状态更新为当前状态加 1。因此，我们可以在每次点击后将计数器加 1。

如果你愿意，你也可以在 [Stackblitz](https://react-7mzbjb.stackblitz.io/) 上观看现场演示。

# useRef 挂钩

挂钩 useRef 有点类似于 useState，它返回一个具有属性 current 的对象，我们可以使用对象点标记法访问该对象。属性 current 接受我们传递给函数 useRef()的参数值。

因此挂钩 useRef 也接受一个参数(属性 current 的初始值)。此外，请记住，返回的对象将在组件的整个生存期内保持不变。

同样，要开始使用钩子，您必须首先从 React 导入它。然后就可以毫无问题的使用了。

```
import React, { useRef } from 'react';
```

让我们试试控制台中的挂钩，看看它是如何工作的:

```
//using useRef and giving it 0 as a parameter.
const ourRef = useRef(0);console.log(ourRef);
  //{ current: 0 }
console.log(ourRef.current); // 0
```

如您所见，useRef 返回一个包含属性的对象，该属性具有我们传递的参数值。我们可以使用对象点符号来访问该值。

useRef 非常强大，因为它在渲染之间是持久的。与 useState 不同，useRef 不会在值或状态改变时导致组件重新呈现。

为了让事情更清楚，我们来看一个实际的例子。我们将向您展示与上面使用 useState 相同的递增计数器示例，但是现在使用 useRef。

下面是一个例子:

```
//import useRef.
import React, { useRef } from 'react'function MyComponent() {
    // Using useRef.
  const ourRef = useRef(0) //JSX.
  return(
      <>
      <h1>{ourRef.current}</h1>
      <button onClick={()=> ourRef.current = ourRef.current + 1}>Increment</button>
      </>
  )
}export default MyComponent;
```

如您所见，我们将初始值设置为 0，并访问返回对象中的属性`current`,以将计数器加 1。现在的问题是，即使我们点击按钮，数字 0 也不会递增。这是因为挂钩 useRef 不会导致组件重新呈现。组件需要呈现才能更新 UI。

如果您在控制台中打印了当前属性的值，您会发现当您单击该按钮时，该值实际上会增加 1。但是它不会显示在 UI 中，因为组件不会被重新呈现。所以 useRef 不是创建计数器的好选择。如果你愿意，你可以在 Stackblitz 上查看现场演示。

# UseRef 用例

使用钩子 useRef 的一个主要用例是在 React 中引用 DOM 元素。DOM 中的每个元素都有一个名为 ref 的属性，我们可以将 ref 设置为这个属性。下面是一个示例，它允许我们在单击按钮后访问输入元素并聚焦于它:

```
const Mycomponent = ()=> {
  const inputRef = useRef(null) const inputFocus = () => {
    inputRef.current.focus()
  } return (
    <>
      <input ref={inputRef} />
      <button onClick={inputFocus}>Focus on the Input</button>
    </>
  )
}
```

useRef 的另一个用例是跨组件呈现持久化的存储。钩子 useRef 允许我们存储状态的前一个值。如果你感兴趣的话，你可以了解更多。

# useState VS useRef

对于使用状态:

*   允许功能组件拥有自己的状态。
*   允许我们更新组件内部的状态。
*   它会导致组件在状态更新后重新呈现。
*   返回当前状态。
*   有一个更新状态的更新函数。

对于 useRef:

*   返回具有包含初始值的属性的对象。
*   当值或状态改变时，不会导致组件重新呈现。
*   数据在渲染之间保持不变。
*   允许引用 DOM 元素。

这就是这两个非常有用的 React 钩子之间的区别。

# 结论

如您所见，挂钩 useState 和 useRef 有点相似。不同之处在于，useState 返回当前状态，并有一个更新状态的 updater 函数。虽然 useRef 返回一个对象，但不会导致组件重新呈现，它用于引用 DOM 元素。

*感谢您阅读本文。此外，如果你觉得我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [*这里*](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得无限制访问媒体上的所有文章，并支持我们作为作家。*

[](https://mehdiouss.medium.com/membership) [## 通过我的推荐链接加入 Medium-Mehdi Aoussiad

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mehdiouss.medium.com](https://mehdiouss.medium.com/membership) 

## **延伸阅读:**

[](/difference-between-find-and-findindex-in-javascript-63204178bbc1) [## JavaScript 中 find()和 findIndex()的区别

### JavaScript 中的 find() vs findindex():你需要知道的一切。

javascript.plainenglish.io](/difference-between-find-and-findindex-in-javascript-63204178bbc1) [](/6-awesome-css-shorthand-properties-that-you-probably-dont-know-f593b21ebf3) [## 你可能不知道的 6 个很棒的 CSS 速记属性

### 每个开发人员都应该知道的有用的 CSS 速记属性列表。

javascript.plainenglish.io](/6-awesome-css-shorthand-properties-that-you-probably-dont-know-f593b21ebf3) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***