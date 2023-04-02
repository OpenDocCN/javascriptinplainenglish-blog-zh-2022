# 如何用 React 钩子向状态数组推送或追加元素？

> 原文：<https://javascript.plainenglish.io/how-to-push-or-append-an-element-to-a-state-array-with-react-hooks-32e75c090040?source=collection_archive---------3----------------------->

![](img/d44f700a12afc64827b9ac5439fd4de3.png)

Photo by [Pierre Bamin](https://unsplash.com/@bamin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在许多情况下，我们可能有数组形式的状态。

我们可能希望将项目推到数组的末尾。

对我们来说，做这件事的方法可能不会马上显而易见。

在本文中，我们将了解如何使用 React 钩子将元素推入或追加到状态数组中。

# 传入一个回调函数，该回调函数向状态设置器函数返回一个新数组

为了在状态数组的末尾添加一个新元素来更新状态数组，我们可以传入一个回调函数，该函数返回一个新的数组，数组的末尾添加了新的元素。

为此，我们写道:

```
import React, { useState } from "react";export default function App() {
  const [arr, setArr] = useState(["foo"]);
  return (
    <div className="App">
      <button onClick={() => setArr((oldArray) => [...oldArray, "foo"])}>
        add
      </button>
      <div>
        {arr.map((a, i) => (
          <p key={i}>{a}</p>
        ))}
      </div>
    </div>
  );
}
```

我们用`useState`钩子定义了`setArr`状态设置函数。

`arr`状态的初始值是一个数组，就像我们在`useState`的自变量中一样。

我们有一个`onClick`处理程序，它用一个接受`oldArray`参数的回调函数调用`setArr`函数，这个参数是`arr`状态的旧值。

我们返回一个数组，其中包含从`oldArray`展开的现有项目和数组末尾的新项目。

在某些情况下，比如点击添加条目，我们也可以将新的数组值直接传递给 state setter 函数。

所以我们也可以写:

```
import React, { useState } from "react";export default function App() {
  const [arr, setArr] = useState(["foo"]); return (
    <div className="App">
      <button onClick={() => setArr([...arr, "foo"])}>add</button>
      <div>
        {arr.map((a, i) => (
          <p key={i}>{a}</p>
        ))}
      </div>
    </div>
  );
}
```

当我们想点击添加一个新的数组条目时。

我们也可以使用`concat`方法返回一个数组，在它的末尾有一个新值。

例如，我们可以写:

```
import React, { useState } from "react";export default function App() {
  const [arr, setArr] = useState(["foo"]); return (
    <div className="App">
      <button onClick={() => setArr((oldArray) => oldArray.concat("foo"))}>
        add
      </button>
      <div>
        {arr.map((a, i) => (
          <p key={i}>{a}</p>
        ))}
      </div>
    </div>
  );
}
```

我们在`oldArray`上调用`concat`，参数是我们想要添加的新项目。

所以我们得到了和以前一样的结果。

# 结论

要在 React 组件状态数组的末尾添加一个新项，我们可以向 state setter 函数传递一个回调，该函数获取旧的数组值并返回新的数组值。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***