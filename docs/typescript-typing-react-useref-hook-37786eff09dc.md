# TypeScript:键入 React useRef 钩子

> 原文：<https://javascript.plainenglish.io/typescript-typing-react-useref-hook-37786eff09dc?source=collection_archive---------3----------------------->

![](img/23670649b92d42b41c5118c0403edf3a.png)

有些情况下，我们需要在通常的组件流之外强制性地修改 React 组件中的 DOM 元素。最常见的例子是在 React 应用程序中管理元素的焦点或使用第三方库(尤其是那些不是用 React 编写的库)。

这篇文章将通过一个控制输入元素焦点状态的例子来演示如何在 TypeScript 中键入`useRef`钩子。

假设我们有一个简单的用例，我们希望手动将输入集中在按钮点击上。组件的 JS 代码如下所示:

当我们点击`Focus input`按钮的时候，`name`输入域就会被聚焦，到目前为止一切顺利。现在我们想为这个组件使用 TypeScript。作为第一步，我们可以简单地将文件的扩展名从`.js`改为`.tsx`。我们将文件转换成 TS 后得到的错误是第`inputRef.current.focus();`行的`Object is possibly null`。这是有意义的，因为我们确实将`null`设置为`inputRef`的初始值。要修复这个错误，我们可以在对其调用`focus`之前检查`inputRef`的`current`属性是否不为空:

```
if (inputRef.current !== null) { 
    inputRef.current.focus(); 
}
```

这可以用[可选链接操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) `?.`简化:

```
inputRef.current?.focus();
```

如果`inputRef.current`为 nullish ( `null`或`undefined`)，则不调用表达式 short-circuits 和`focus`方法(如果我们将调用的结果赋给一个变量，那么在这种情况下它将被设置为`undefined`)。

这修复了类型错误，但是，它创建了一个新的错误- `Property 'focus' does not exist on type 'never'.`这起初看起来很奇怪，因为我们稍后会将 ref 分配给 input 元素。问题是 TS 从缺省值推断出`inputRef`不能是除了`null`之外的任何值，并将相应地键入它。但是我们知道 ref 稍后将包含一个 input 元素，所以要解决这个问题，我们需要明确地告诉编译器需要哪种类型的元素:

```
const inputRef = useRef<HTMLInputElement>(null);
```

这解决了问题，我们没有得到任何类型错误。最终代码如下所示:

# useRef <htmlinputelement>(空)vs useRef <htmlinputelement null="">(空)</htmlinputelement></htmlinputelement>

对于我们不需要重新分配其值的情况，`inputRef`的当前类型工作得很好。让我们考虑这样一种情况，我们想要手动添加一个事件监听器到一个输入中(在使用第三方库时很有用)。代码看起来会像这样:

注意，我们需要将`document.getElementById`的结果转换为`HTMLInputElement`，因为 TS 在这种情况下无法推断出正确的元素类型，而是默认为更通用的`HTMLElement`。但是我们知道这个例子中的元素是一个输入元素，所以对它进行相应的转换是安全的。虽然代码看起来不错，但是我们得到了一个 TS 错误- `Cannot assign to 'current' because it is a read-only property.`。在检查`current`属性时，我们看到它的类型被定义为`React.RefObject<HTMLInputElement>.current:any`。深入到`React.RefObject`的类型定义，它被定义为:

```
interface RefObject<T> { readonly current: T | null; }
```

那么如何才能让它变得可变呢？按照`useRef`的类型定义，我们看到它实际上有一些重载，其中最重要的是:

```
function useRef<T>(initialValue: T): MutableRefObject<T>; 
function useRef<T>(initialValue: T | null): RefObject<T>;
```

当将`null`指定为默认参数，但不将其包含在 type param 中时，我们为`useRef`匹配第二个重载，获得一个具有 readonly `current`属性的 ref 对象。要修复它，我们需要在类型参数中包含`null`:

```
const inputRef = useRef<HTMLInputElement | null>(null);
```

这将匹配`MutableRefObject`重载并修复类型问题。在钩子的类型定义中还有一个方便的注意事项:

```
Usage note: if you need the result of useRef to be directly mutable, include | null in the type of the generic argument.
```

代码的最终版本如下:

*原载于*[*https://claritydev.net*](https://claritydev.net/blog/typescript-typing-react-useref-hook/)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****