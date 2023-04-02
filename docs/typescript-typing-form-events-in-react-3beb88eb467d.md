# TypeScript:在 React 中键入表单事件

> 原文：<https://javascript.plainenglish.io/typescript-typing-form-events-in-react-3beb88eb467d?source=collection_archive---------15----------------------->

![](img/f05fe588a5644fc2eaba1e7e45f231c2.png)

React 中处理事件的方式与 DOM 元素上处理事件的方式非常接近。

有一些小的区别，例如，事件名称遵循 camel 大小写约定，而在 DOM 中它们都是小写的；函数本身作为事件处理程序传递，而不是以字符串形式传递其名称。

然而，最大的区别是，React 将原生 DOM 事件包装到`SyntheticEvent`中，使它们的行为与原生事件略有不同。 [React 的文档](https://reactjs.org/docs/events.html)详细解释了合成事件的来龙去脉。因此，在 React 中键入表单事件与本地事件不同，React 提供了自己的类型。在这篇文章中，我们将看到如何在 React 中以一个简单的组件为例输入表单事件，并讨论最常见的陷阱。

让我们以这个简单的注册表单为例:

如果我们想收集表单数据并将其发送到服务器，有两个主要选项。第一个是保持表单不受控制并在`onSubmit`回调中获取数据，第二个是存储表单状态的数据并在表单提交时发送。我们将在这里考虑这两种方法。

# 非受控形式

为了在提交时获取表单数据，我们将添加`onSubmit`回调，并通过其`name`属性从每个元素中检索数据。

为了简单起见，我们在这里省略了数据验证和错误处理(以及 CSS 样式)。重要的叫`event.preventDefault()`；首先，因为表单提交将在我们收集数据之前重新加载页面。从回调返回`false`在这里不起作用，这是合成事件和原生 DOM 事件的区别之一。为了收集表单数据，我们可以通过元素的 id 或者目标的`elements`属性直接从事件的目标访问它，例如`email: event.target.email.value`和`email: event.target.elements.email.value`都工作。也可以使用`name`属性来获取表单元素的值，但是因为我们已经设置了 id(通过`htmlFor`属性将我们的输入连接到它们的标签)，我们将在这里使用`id`。

您会注意到事件的类型是`any`,这意味着现在没有类型检查。为了解决这个问题，我们需要为`onSubmit`回调定义事件的类型。对于合成事件，我们将使用 React 提供的类型定义。第一种选择是使用带有`HTMLFormElement`类型参数的`React.FormEvent`。这种方法虽然通常是正确的，但对我们的表单并不适用，因为我们想要从`target`属性中检索数据，该属性获得通用的`EventTarget`类型。这是因为`FormEvent`类型最终归结为`BaseSyntheticEvent<E, EventTarget & T, EventTarget>`，其中最后一个`EventTarget`参数用于`target`属性类型。似乎我们无法控制目标属性的类型，即使我们控制了(如果需要，我们总是可以断言类型),它仍然不知道我们的表单有哪些表单元素。深入查看`BaseSyntheticEvent`的类型定义，我们可以看到第二个类型参数`EventTarget & T`被分配给事件的`currentTarget`属性。似乎要解决我们的类型问题，我们只需要从`event.target`切换到`event.currentTarget`。

如果表单中没有 id 为`name`的 input 元素，这个*几乎*也能正常工作。目前，我们的`currentTarget.name`覆盖了`HTMLFormElement`的`name`属性。然而，这种方法有一个更大的问题，那就是缺乏对目标属性的正确类型检查。例如，我们可以尝试通过`address: target.address.value`访问一个不存在的表单元素，它不会被 TS 捕获，因为它不知道表单中有什么元素。如果我们能够定义 id - element 对并相应地键入当前目标，那就更好了。为此，我们需要研究一下`HTMLFormElement`的类型定义。我们可以看到它有`readonly elements: HTMLFormControlsCollection;`，有随手可得的文档——`Retrieves a collection, in source order, of all controls in a given form`。这是我们之前讨论过的`event.target.elements`属性，除了在这种情况下它在`currentEvent`上。

连接一切，看起来我们可以用表单元素扩展`HTMLFormControlsCollection`，然后用那个接口覆盖`HTMLFormElement.elements`。

这解决了类型问题，并在访问表单元素的值时提供了正确的类型检查。

# 受控形式

虽然知道如何正确地键入不受控制的表单的事件处理程序很有用，但这种表单在 React 组件中并不常见。大多数情况下，我们希望表单包含受控元素，这些元素的值/回调也可以来自父组件。在这种情况下，通常将表单值保存到组件的状态，然后在提交表单时将它们发送到服务器，甚至不使用表单的 submit 事件。幸运的是，键入这样的事件处理程序比上面的例子更简单。

例如，让我们将用户输入的值保存到状态中，然后在用户单击`Sign up`时通过 API 发送它们。为了简单起见，我们将使用一个状态对象(类似于状态在基于类的组件中的保存方式)。

通常最好使用`useReducer`钩子来处理复杂的状态，但是,`useState`适用于本演示。为了更新表单元素的状态值，我们需要为每个字段分配`onChange`处理程序。这里最明显的做法是给每个元素分配不同的`onChange`处理程序，例如:

然而，有一种更简单的方法。类似于表单的 submit 事件将所有元素 id 或名称保存到目标中，change 事件的目标具有`name`和`id`属性，可以用来将相应元素的值分配给状态。由于我们已经在字段上定义了 id(这些 id 与我们收集数据的字段同名)，我们将使用它们将字段数据与州匹配。不过这种方法有一个小问题，那就是我们有一个复选框元素。对于复选框元素，我们寻找的是`checked`属性，而不是`value`。在这种情况下，每个元素类型都有一个单独的处理程序是可以的，例如`onInputChange`和`onCheckboxChange`，但是，因为我们有一个只有一个复选框的简单表单，所以让我们给处理程序添加一个条件，它将根据目标的类型检索复选框字段的`checked`属性。

注意，对于提交事件，我们还恢复到了`FormEvent<HTMLFormElement>`类型，因为我们不再访问它的值。现在我们只需要输入`onChange`事件。最初，我们试图将事件类型化为`React.ChangeEvent`，但是这似乎还不够，因为我们得到了一个类型错误，即我们试图访问的所有属性在事件的目标上都不存在。查看`ChangeEvent`的定义，我们可以看到它接受类型参数，默认为泛型`Element`。因为表单的所有元素都是输入，我们将把这个类型传递给`ChangeEvent` - `const onFieldChange = (event: ChangeEvent<HTMLInputElement>) => {`。现在，所有目标的属性都被正确识别了，但是，当将`event.target.checked`重新分配给值- `Type 'boolean' is not assignable to type 'string'`时，出现了一个新问题。这是因为当我们用`let value = event.target.value;`声明 value 时，TS 推断它的类型是 string，这是输入值的类型。为了解决这个问题，我们需要让 TS 知道我们的值也可以是一个布尔值:`let value: string | boolean = event.target.value;`。这工作得很好，但是，如果 TS 能根据状态自动推断出值的类型不是更好吗？例如，假设我们添加了一个新字段`age`，它输入了一个类型号。为了将它保存到 state 中，我们将这个块添加到`onFieldChange`:

为了消除 TS 错误，我们必须将值的类型更新为`boolean | string | number`。但是如果我们最终决定删除年龄字段呢？我们还需要记住再次更新值类型。我们可以定义一个单独的`State`类型，在这里我们声明所有字段的类型，然而，有一个更好的方法。我们已经从状态中获得了状态值的类型，并且我们知道这些类型是每个字段仅有的类型。在这种情况下，最好从现有数据中推断出类型，因为这样会在数据结构发生变化时自动保持它们的同步。为了从状态中推断出类型，我们可以使用简洁的 TS 符号- `let value: typeof state[keyof typeof state] = event.target.value;`。这里我们告诉 TS，我们期望`value`是状态上存在的值的类型，如果将来它们中的任何一个发生变化，这些变化将自动反映在`value`的类型中。表单的最终代码如下所示:

*原载于*[](https://claritydev.net/blog/typescript-typing-form-events-in-react/)**。**

**更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。****