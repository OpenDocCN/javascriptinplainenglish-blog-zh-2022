# 为什么您可能选择使用 useRef 而不是 useState

> 原文：<https://javascript.plainenglish.io/why-you-might-choose-to-use-useref-instead-of-usestate-4950f0ab7687?source=collection_archive---------4----------------------->

您可能选择使用 useRef 而不是 useState 有几个原因:

![](img/3f8695a1e474a63bd50f422491434974.png)

-存储不需要触发重新呈现的值:如前所述，无论何时状态值改变，useState 都会触发重新呈现，而 useRef 在值改变时不会触发重新呈现。如果您需要存储一个在发生变化时不需要触发重新呈现的值，useRef 可能是更好的选择。

-直接改变一个值:useRef 创建一个值的可变引用，这意味着您可以通过访问 Ref 的 current 属性直接修改该值。另一方面，useState 只允许您通过调用钩子返回的 update 函数来更新状态值。如果需要直接变异一个值，useRef 可能是更好的选择。

-存储需要跨多个渲染周期访问的值:useRef 允许存储可以跨多个渲染周期访问的值，而 useState 只存储当前状态值。如果需要存储一个需要跨多个渲染周期访问的值，useRef 可能是更好的选择。

该示例演示了如何使用 useRef 来存储输入字段的值:

```
import { useRef } from 'react';

function Example() {
  const inputEl = useRef(null);

  const handleSubmit = event => {
    event.preventDefault();
    console.log(inputEl.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={inputEl} type="text" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

在这个例子中，我们使用 useRef 创建对 input 元素的引用。然后，我们将引用传递给输入元素的 ref prop。这允许我们在提交表单时访问输入字段的值。

如果您需要存储输入字段的值并在以后访问它，而不需要在值更改时触发重新呈现，那么以这种方式使用 useRef 会很有用。

如何使用 useState 而不是 useRef 实现相同的示例:

```
import { useState } from 'react';

function Example() {
  // Declare a state variable to store the input value
  const [inputValue, setInputValue] = useState('');

  const handleSubmit = event => {
    event.preventDefault();
    console.log(inputValue);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={inputValue}
        onChange={event => setInputValue(event.target.value)}
        type="text"
      />
      <button type="submit">Submit</button>
    </form>
  );
} 
```

在本例中，我们使用 useState 将输入字段的值存储在一个状态变量中。然后，我们使用 value 和 onChange 属性将输入字段绑定到状态变量。这允许我们在提交表单时访问输入字段的值，并在输入字段的值发生变化时更新状态。

如果您需要存储输入字段的值并在值更改时触发重新呈现，以这种方式使用 useState 会很有用。但是，请记住，只要输入字段的值发生变化，使用 useState 就会触发重新呈现，这在某些情况下可能是不可取的。在这些情况下，您可能需要考虑使用 useRef。

请记住，useRef 和 useState 服务于不同的目的，最好在不同的上下文中使用。根据您的需要选择合适的钩子很重要，这样可以确保您的代码既有效又高效。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***