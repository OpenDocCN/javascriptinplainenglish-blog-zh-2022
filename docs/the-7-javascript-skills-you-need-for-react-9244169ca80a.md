# React 需要的 7 个 JavaScript 技能

> 原文：<https://javascript.plainenglish.io/the-7-javascript-skills-you-need-for-react-9244169ca80a?source=collection_archive---------1----------------------->

## 它们是如何工作的，以及它们为什么重要

![](img/dd66a5e1173b2810e79d09a25e30e0a6.png)

Image generated with MidJourney

JavaScript 的基础知识和你在 React 中理解编码所需要的东西之间存在差距。请注意，这不是一个巨大的黑洞，但足以让它值得探索。以下是你在 React 中需要掌握的 7 个 JavaScript 技巧。

我们将讨论它们如何出现在 React 中，以及它们如何对您有用。用于不变性、条件呈现、显示组件列表等等。

即使你对 React 不感兴趣，你仍然需要这些概念来编写好的 JavaScript 代码。

但是首先…

# 1.真实与虚假

一个快速但基本的观点。JavaScript 认为某些值是“假的”。虽然他们不是`false`，但是他们仍然失败了一个`if`语句。换句话说，JavaScript 的行为就好像这些值是假的一样。

JavaScript 中的 Falsy 值包括(除其他外):

*   不明确的
*   空
*   空字符串
*   空数组
*   0
*   NaN(或者不是一个数字)

这有助于理解布尔运算符和三元运算符…

# 2.布尔运算符

毫无疑问，您熟悉在条件中使用布尔运算符`&&`和`||`。JavaScript 允许你做的远不止这些。你看，这些操作符并不总是返回一个布尔值。

让我解释一下。

让我们从布尔 or 运算符(`||`)开始。这将计算表达式的第一个元素，并查看它是否为“falsy”。如果值为“真”，则运算符返回第一个词，即运算符左侧的词。如果不是，它返回第二个。

假设我们有一个变量(例如，`name`)。我们不知道它是否被设置。如果*没有*设置，我们要设置一个默认值。or 运算符允许我们执行以下操作:

```
let defaultedName = name || "defaultName";
```

如果`name`为`undefined`或`null`或空字符串，运算符将返回第二项:`"defaultName"`。如果`name` *定义了*，则由操作员返回。这允许我们设置一个默认值。

&&布尔运算符的行为正好相反。如果第一项是“真”，则&&运算符返回第二项。让我们看看如何在 React 中使用它。假设我们有一个变量叫做`errorMessage`。它可能包含也可能不包含错误消息。

在 React 的 JSX 部分，我们可以这样写:

```
{errorMessage && <span>{errorMessage}</span>}
```

在这种情况下，如果 errorMessage 变量为 true，则&&运算符仅返回 span。如果有错误，我们只显示跨度。

# 3.三元运算符

有一个精简的 if / else 语句叫做三元运算符。它是这样工作的，带有一个问号和一个冒号:

```
variableTruthy ? itIsTrue : itIsFalse
```

操作符所做的是检查变量是否“真”。如果是，运算符返回问号后的第一个词。如果不是，则返回冒号后的词。在我们的错误示例中，如果我们还想在没有错误时显示一条消息，我们可以在 JSX 代码中添加以下内容:

```
{ error ? <span>{error}</span> : <span>"There is no error"</span>}
```

当然，在这种特殊情况下，我们可以在 span 中写得更简单:

```
<span>{error ? error : "There is no error"}</span>
```

…但这只是因为我没有费心为这个错误添加任何样式。

# 4.析构数组和对象

让我们来看一个简单的`useState`钩子。

```
const [counter, setCounter] = useState(0);
```

看看`counter`和`setCounter`变量是如何定义的。它们是从数组中定义的。实际上，我们正在将变量映射到`useState`的返回。钩子返回一个数组。此语法将数组的第一个值赋给第一个变量，第二个值赋给第二个变量。

这是一种更简短(也更优雅)的书写方式:

```
const temp = useState(0);
const counter = temp[0];
const setCounter = temp[1];
```

如您所见，重组语法更加简洁，并且去掉了临时变量。对象的语法是相似的。它通常首先出现在 import 语句中。例如:

```
import { useState } from 'react';
```

它是如何工作的？假设我们有一个有年龄和名字的用户对象:

```
const user = {
  name: "Bob", 
  age: 42
}
```

我们可以使用析构直接检索名称:

```
const {name} = user;
```

这相当于

```
const name = user.name;
```

# 5.箭头功能

箭头函数是编写函数的一种更简洁的方式。在 React 中，简洁有助于编写可读的代码。箭头函数也是编写 useEffect 钩子的自然方式。

简单回顾一下:编写函数的“正常”方式是使用`function`关键字。例如:

```
function add(a,b) {
  return a + b;
}
```

我们可以把它写成一个箭头函数，声明如下:

```
const add = (a,b) => {
  return a + b;
}
```

事实上，由于这个函数中只有一个`return`语句，我们可以去掉括号和`return`语句本身:

```
const add = (a,b) => a + b
```

这在使用数组函数时尤其有用。

# 6.数组函数，特别是映射和过滤

数组有一些有趣的函数可以对它们进行操作。我发现 React 中有两个特别有用的特性:`map`和`filter`。

这两个函数都将一个函数作为参数，并返回一个新数组。

Filter 返回一个数组，该数组只包含函数作为参数传递的返回真值的项。

如果我们用返回模 2 的函数过滤一个数字数组，我们的新数组现在只包含奇数。这是因为当运行模运算时，偶数返回 0，而 0 是假的:

```
const odd = [1, 2, 4, 7, 9, 22].filter((a) => a % 2);
// odd now only has odd numbers :  [1, 7, 9]
```

另一方面，Map 返回一个数组，其中每个新项都是函数的返回值。如果我们传递一个将其输入乘以 2 的函数，那么输出就是输入的双精度数组。

```
const double = [1, 2, 4, 7, 9, 22].map((a) => a * 2);
// double now has doubles:  [2, 4, 8, 14, 18, 44]
```

这在 React 中如何有用？假设我们正在构建一个待办事项列表应用程序。我们有一个想要显示的任务数组，存储在一个`tasks`变量中。每个项目都有(例如) :

*   一个身份证，
*   一个标题，
*   完成状态，可以是真或假。

假设我们已经定义了一个任务组件。我们可以使用 map 函数创建一个列表，为每个项目返回一个任务组件:

```
{ tasks.map((task) => <Task key={task.id} task={task} /> }
```

通过使用`filter`隐藏 complete 为真的项目，我们可以只显示不完整的项目:

```
{ 
tasks.filter(task => !item.complete).map((task) => <Task key={task.id} task={task} /> 
}
```

(小题外话:我们需要指定一个`key`值来帮助 React 跟踪到底发生了什么变化。)

还有许多其他有用的数组函数值得一提。这个问题值得更深入的研究。但这两个是我觉得最有用的。

# 7.扩展运算符(和对象属性简写)

如果在您的状态中使用对象，您需要开始使用 spread 操作符。spread 操作符允许我们创建一个具有相同值的复制对象。

```
const user = {
  name: "Bob", 
  age: 42
}

const user1 = user;
const user2 = {...user};

console.log(user == user1); // true 
console.log(user == user2); // false
```

这为什么有用？React 跟踪更改，以了解何时重新渲染组件树的各个部分。在上面的例子中，`user`和`user1`是同一个对象。

例如，如果我们在`user1`上将`age`属性设置为 43，`user1`仍将等于`user`。

现在，想象 React 正在跟踪`user`对象的状态。更改用户对象的一个属性值不会触发状态更改的检测。假设我们有一个用于更新用户状态的`setUser`函数。如果我们这样做:

```
user.age = 43;
setUser(user);
```

这不会触发更改检测。`user`对象仍然是完全相同的对象。我们需要使用 spread 操作符创建一个新的对象，因此:

```
setUser({...user, age: 43});
```

这里发生了什么？

两个花括号意味着我们已经创建了一个新对象。“扩展”操作符的作用就像它拆分(或扩展)初始对象一样。

如果我们要明确地写这里发生了什么……那将会特别冗长。我们需要首先创建一个空白的新对象。然后我们列出`user`对象上的所有键。然后我们遍历键列表。这样做时，我们将新对象中的属性值设置为旧对象中的相应值。最后，我们设置新的更改值。

```
const newUser = {}
let keys = Object.keys(user); 

for(let i = 0; i < keys.length; i++) {
	let key = keys[i];
	newUser[key] = user[key];
}

newUser.age = 43;
```

一点也不简洁。

spread 运算符将所有内容压缩成一行。一旦你理解了它的意思，产生的代码也是可读的(如果不是更可读的话)。

# 采取下一步措施

记住:使用一门语言的高级特性永远不应该超过可读性。然而，如果使用正确，这些特性有助于使你的代码更具可读性，而不是更差。

还有什么要掌握的，要不断学习？

首先，理解[承诺和异步/等待是如何工作的](/what-are-javascript-promises-how-to-use-them-84fdff5757b9)至关重要。这不是*反应堆的核心*部分。有些钩子为你隐藏了复杂性。但如果你想掌握 JavaScript，这是不可避免的。

如果你希望掌握 React，你需要了解钩子如何工作，[以及初学者应该避免的错误](https://medium.com/p/ed137b148f5a)。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***