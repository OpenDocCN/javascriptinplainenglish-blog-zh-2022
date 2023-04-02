# 如何在 React 中触发一个组件用钩子重新渲染？

> 原文：<https://javascript.plainenglish.io/how-to-trigger-a-component-to-re-render-with-hooks-in-react-b78061c6be54?source=collection_archive---------1----------------------->

![](img/ec07b6ad2c4c1897e20a67c109a42092.png)

Photo by [Pascal Bernardon](https://unsplash.com/@pbernardon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望触发一个组件，在用 React 钩子创建的组件中重新呈现。

在本文中，我们将研究如何触发一个组件在用钩子创建的 React 组件中重新呈现。

# 更新道具或状态

如果属性或状态值改变，组件将重新呈现。

因此，我们可以在更新属性或状态值时触发组件的重新呈现。

为了更新状态，我们调用状态设置函数。

例如，我们可以写:

```
import React, { useState } from "react";export default function App() {
  const [count, setCount] = useState(0); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

添加一个调用`setCount`来更新`count`状态的按钮。

我们知道`App`组件被重新渲染了，因为当我们点击增量按钮时`count`的最新值显示在它的下面。

同样，我们可以更新一个适当值来触发组件的重新呈现。

例如，我们可以写:

```
import React, { useState } from "react";const Count = ({ count }) => <p>{count}</p>;export default function App() {
  const [count, setCount] = useState(0); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <Count count={count} />
    </div>
  );
}
```

我们有接受`count`道具并呈现`count`值的`Count`组件。

为了使`Count`组件重新呈现，我们通过更新`App`中`count`状态的值来更新`count`属性的值。

这部分和前面的例子一样。

并且我们知道`Count`被重新渲染，因为我们看到了再次渲染的`count`的最新值。

# 强制重新呈现 React 组件

有时，当组件外部的某些内容被更新时，我们可能希望强制 React 组件重新呈现。

为此，我们可以创建自己的钩子。

例如，我们可以写:

```
import React, { useCallback, useState } from "react";let count = 0;setInterval(() => {
  count++;
}, 1000);const useForceUpdate = () => {
  const [, setTick] = useState(0);
  const update = useCallback(() => {
    setTick((tick) => tick + 1);
  }, []);
  return update;
};export default function App() {
  const update = useForceUpdate(); return (
    <div className="App">
      <button onClick={() => update()}>update</button>
      <p>{count}</p>
    </div>
  );
}
```

我们有一个`setInterval`回调函数来设置`count`变量的值。

我们创建了一个用`setTick`函数更新状态的`useForceUpdate`钩子。

`setTick`在我们返回的`update`函数中被调用，因此我们可以在组件代码中使用它。

在`App`中，我们调用`useForceUpdate`来将返回值赋给`update`变量。

然后在按钮中，当我们点击它时，我们调用`update`。

因此，当我们点击它时，我们看到显示的是`count`的最新值。

# 结论

有几种方法可以用 React 挂钩触发 React 组件的重新渲染。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*