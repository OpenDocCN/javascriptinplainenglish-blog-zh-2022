# React 组件中 useRef 和 createRef 有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-useref-and-createref-in-a-react-component-4d091b8a1fe7?source=collection_archive---------9----------------------->

![](img/eb5de58ca9765db7934949c6adacf62e.png)

Photo by [Eric Prouzet](https://unsplash.com/@eprouzet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 React 组件中，我们可以使用`useRef`钩子或者`createRef`函数来创建一个 ref。

ref 是一个值，当组件改变时，它不会触发组件的重新呈现，这与状态和属性相反。

在本文中，我们将看看 React 组件中的`useRef`钩子和`createRef`函数之间的区别。

# useRef 和 createRef 之间的区别

`useRef`钩子和`createRef`函数的区别在于`useRef`钩子在函数组件的重新渲染之间保持它的值。

现有的引用在重新渲染之间保持不变。

`createRef`用于创建一个参考，每次渲染时创建一个新的参考。

例如，如果我们有:

```
import React, { createRef, useEffect, useState } from "react";export default function App() {
  const [count, setCount] = useState(0);
  const ref = createRef(); useEffect(() => {
    ref.current = "foo";
  }, []); useEffect(() => {
    console.log(count, ref.current);
  }, [count]); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

我们用`createRef`创建一个 ref。

我们只在初始渲染时设置了`ref.current`。

为了触发重新渲染，我们在点击按钮时更新`count`状态。

我们可以从控制台日志的`useEffect`回调中看到`ref.current`在第一次渲染时记录了`'foo'`。

但随后在后续渲染时，`ref.current`就是`null`。

另一方面，如果我们通过编写使用`useRef`钩子:

```
import React, { useEffect, useRef, useState } from "react";export default function App() {
  const [count, setCount] = useState(0);
  const ref = useRef(); useEffect(() => {
    ref.current = "foo";
  }, []); useEffect(() => {
    console.log(count, ref.current);
  }, [count]); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

我们调用`useRef`钩子来创建一个 ref。

我们像前面的例子一样设置`ref.current`。

其余的代码也是一样的。

不同的是，每次渲染后我们看到的`ref.current`是`'foo'`。

这意味着在函数组件中，我们可以使用`useRef`钩子来创建一个值，当它改变时不会触发重新渲染，但是我们可以用它来保持重新渲染之间的值。

# 结论

`createRef`和`useRef`的区别在于`createRef`会在函数组件中的每次渲染时创建一个新的 ref。

另一方面，用`useRef`创建的 ref 在函数组件中每次渲染后都保持相同的值。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*