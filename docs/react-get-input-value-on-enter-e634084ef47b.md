# 在 React 中按下 Enter 键时获取输入的值

> 原文：<https://javascript.plainenglish.io/react-get-input-value-on-enter-e634084ef47b?source=collection_archive---------10----------------------->

## 一个关于如何在 React 中按下 Enter 键时轻松获取输入字段值的教程。

![](img/a5160bf3f59bb52f50705543cff78f1f.png)

要在 React 中按下 Enter 键时获取输入值:

1.  创建一个状态变量来存储输入的值。
2.  在输入上设置一个`onChange`事件处理程序，以便在输入字段值改变时更新状态变量。
3.  在输入上设置一个`onKeyDown`事件处理程序。
4.  在检查按下的键是 Enter 之后，使用状态变量访问事件处理程序中的输入值。

例如:

`App.js`

```
import { useState } from 'react';export default function App() {
  const [message, setMessage] = useState(''); const [updated, setUpdated] = useState(''); const handleChange = (event) => {
    setMessage(event.target.value);
  }; const handleKeyDown = (event) => {
    if (event.key === 'Enter') {
      // 👇 Get input value
      setUpdated(message);
    }
  }; return (
    <div>
      <input
        type="text"
        id="message"
        name="message"
        value={message}
        onChange={handleChange}
        onKeyDown={handleKeyDown}
      /> <h2>Message: {message}</h2> <h2>Updated: {updated}</h2>
    </div>
  );
}
```

![](img/4d8cbdc25950ec9ce04058aa912134f5.png)

使用`useState()`钩子，我们创建一个状态变量(`message`)来存储输入字段的当前值。我们还创建了另一个状态变量(`updated`)，当 Enter 键被按下时，它将被输入字段值更新。

我们在输入字段上设置了一个`onChange`事件处理程序，以便在输入值改变时调用这个处理程序。在处理程序中，我们使用`event`对象的`target`属性来访问表示`input`元素的对象。该对象的`value`属性包含输入值，因此我们将其传递给`setMessage()`以更新`message`，这反映在页面上。

在设置了受控输入之后，我们现在可以在`handleChange`处理程序之外使用`message`来访问输入字段的当前值。

我们使用`event.key`属性在`onKeyDown`事件处理程序中获取按键。确保该键被输入后，我们使用`setUpdated(message)`用当前输入字段值更新`updated`变量。

# 用`event.target`回车获取输入值

我们还可以使用`Event`对象的`target.value`属性来获取输入的值。这在我们没有用状态变量跟踪输入值的情况下是有用的，例如，不受控制的输入。

```
import { useState } from 'react';export default function App() {
  const [updated, setUpdated] = useState(''); const handleKeyDown = (event) => {
    if (event.key === 'Enter') {
      setUpdated(event.target.value);
    }
  }; return (
    <div>
      <input
        type="text"
        id="message"
        name="message"
        onKeyDown={handleKeyDown}
      /> <h2>Updated: {updated}</h2>
    </div>
  );
}
```

![](img/db404aafa91ef6276bac01632724fb7b.png)

# 用 ref 输入时获取输入值

当 Enter 键被按下时，我们也可以使用 ref 来获取非受控输入的值。

```
import { useRef, useState } from 'react';export default function App() {
  const inputRef = useRef(null); const [updated, setUpdated] = useState(''); const handleKeyDown = (event) => {
    if (event.key === 'Enter') {
      setUpdated(inputRef.current.value);
    }
  }; return (
    <div>
      <input
        ref={inputRef}
        type="text"
        id="message"
        name="message"
        onKeyDown={handleKeyDown}
      /> <h2>Updated: {updated}</h2>
    </div>
  );
}
```

受控输入中的数据由 React state 处理，而非受控输入中的数据由 DOM 本身处理。这就是为什么上面例子中的`input`没有设置`value`道具或`onChange`事件处理程序。相反，我们使用 React ref 访问输入字段值。当输入中的文本发生变化时，DOM 会更新这个值。

我们用`useRef()`钩子创建一个 ref 对象，并将其设置为`input`的`ref`道具。这样做将 ref 对象的`current`属性设置为表示`input`元素的 DOM 对象。

`useRef()`返回一个可变的 ref 对象，该对象在组件更新时不改变值。此外，修改该对象的`current`属性值不会导致重新渲染。这与从`useState()`返回的`setState`更新功能相反。

尽管 React 文档建议使用受控组件，但非受控组件也有一些优势。如果表单非常简单，不需要即时验证，并且只需要在提交表单时访问值，那么您可能更喜欢使用它们。

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/c57a52)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。