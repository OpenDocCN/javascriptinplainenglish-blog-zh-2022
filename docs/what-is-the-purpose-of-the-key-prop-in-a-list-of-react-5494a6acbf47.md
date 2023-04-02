# 了解 React.js 中数组子项的唯一性

> 原文：<https://javascript.plainenglish.io/what-is-the-purpose-of-the-key-prop-in-a-list-of-react-5494a6acbf47?source=collection_archive---------5----------------------->

在 React 中，key prop 用于惟一地标识组件列表中的元素。为列表中的每个元素提供一个 key prop 是很重要的，因为它允许 React 通过识别哪些项已经更改并只更新那些项来优化呈现，而不是重新呈现整个列表。这可以提高应用程序的性能，特别是对于包含大量项目的列表。

![](img/9db31028c108df6b211143cf43c2bcae.png)

key prop 的值在列表项中应该是唯一的，并且不应该改变。如果可以的话，使用项目的 id 作为键值通常是一个好主意。如果列表项没有惟一的 id，您可以使用列表中项的索引作为键值，但是这通常被认为是一种反模式，因为如果列表顺序改变，它会导致意外的行为。

如何在组件列表中使用 key prop 的示例:

```
const todoList = [
  { id: 1, task: 'Take out the trash' },
  { id: 2, task: 'Do the dishes' },
  { id: 3, task: 'Do the laundry' }
];

const TodoItem = ({ todo }) => (
  <li key={todo.id}>
    <input type="checkbox" />
    {todo.task}
  </li>
);

const TodoList = ({ todos }) => (
  <ul>
    {todos.map(todo => (
      <TodoItem key={todo.id} todo={todo} />
    ))}
  </ul>
); 
```

在这个例子中，我们使用 TodoList 组件呈现一个 todo 项目列表。列表中的每个 todo 项都使用 todo item 组件呈现，并且 key prop 被设置为 todo 项的 id。这允许 React 根据需要正确识别和更新列表中的每个 todo 项。

需要注意的是，key prop 应该只在组件列表的上下文中使用，而不应该作为一种通用的方法来标识组件。如果您需要以一种与列表无关的方式标识一个组件，那么您应该考虑使用一个惟一的 id 属性或者一些其他的惟一标识符。

如果您没有为组件列表中的元素指定 key prop，React 仍将呈现该列表，但它将无法通过识别哪些项目已更改来优化呈现。这可能会导致性能下降，尤其是对于包含大量项目的列表。

此外，如果列表顺序发生变化，不指定 key prop 可能会导致意外的行为，因为 React 将无法正确识别哪些项目已经移动。这可能导致错误的项目被更新或删除，或者新项目被插入到错误的位置。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****想看看你的软件启动规模*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。**