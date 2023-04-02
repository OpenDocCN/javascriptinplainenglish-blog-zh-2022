# SolidJS 对比 React:还能更好吗？

> 原文：<https://javascript.plainenglish.io/solidjs-in-contrast-to-react-could-it-be-better-1aad3ad0f169?source=collection_archive---------1----------------------->

## 了解 SolidJS 和 React 的区别。

![](img/c238e05b96969b9e526851007616585a.png)

这不是一篇关于 Solid JS 与 React JS 的文章，而是一篇帮助您理解 Solid JS 并了解 React 开发人员的区别的文章。在开发社区中看到框架的比较是很常见的，有时很有趣，有时很私人化，但是接近框架的最好方法是把它们仅仅看作工具。您想要构建什么应该会影响使用哪个工具，或者您知道如何使用哪个工具应该会影响您接下/从事什么项目。

够了。

# **什么是固体 JS？**

Solid 是一个**反应式** JavaScript 框架，用于制作交互式网络应用。使用 Solid，您可以使用现有的 HTML 和 JavaScript 知识来构建可以在整个应用程序中重用的组件。Solid 提供了增强组件反应能力的工具:声明性的 JavaScript 代码，将用户界面与它使用和创建的数据联系起来。

# 固体 JS 中的组件

与 React 一样，组件是接受 props 对象并返回 JSX 元素(包括原生 DOM 元素和其他组件)的函数。实际上，组件是为了更好的模块化和可重用性。

```
function SimpleComponent(props) {
  return <div>Hello {props.name}</div>;
}

<SimpleComponent name="Joseph"/>;
```

Solid JS 中的组件不是有状态的，它们不拥有自己的状态，也不依赖于状态。它们主要是用来构建/组织 JSX 元素或者你的代码。因此，它们可以存在，也可以不存在。

同样令人高兴的是，组件函数被调用一次后就不复存在了，这意味着你不需要担心像 ReactJS 中那样意外的重新呈现。所有更新由**固体反应系统**应用。

# 固体 JS 中的反应性

固体的惊人反应取决于*信号*、*备忘录*和*效果*。React 中的钩子通常带有前缀 **use (** *如 useState、useEffect、useMemo 等)*、Solid 中的钩子通常带有前缀 **create** 。

## 信号

类似于 React 中的**状态，信号是固体中反应性的基石。它们包含随时间变化的值；当你改变一个信号的值时，它**会自动**更新任何使用它的东西。**

信号的值开始等于传递的第一个参数`initialValue`(如果没有参数，则为`undefined`)。`createSignal`函数返回一对函数， **getter** 和 **setter** 函数读取和更新值。

```
const [count, setCount] = createSignal(0);

// to update the value of count
setCount(1);
```

*Solid 的 signals setter 函数(****set count****)也接受一个函数形式，可以使用前一个值来设置下一个值。*

```
setCount(c => c + 1);
```

作为函数调用 getter(如`count()`)返回信号的当前值。这与 ReactJs 相反，react js 将 getter 直接用作变量。

```
const App = () => {
  const [count, setCount] = createSignal(0);

  return <div>{count()}</div>;
};
```

***更多关于信号…***

使用上面的代码示例，Solid 自动跟踪对***count()****的任何调用，并在其值发生变化时更新它。Solid 称之为粒度更新。同时在 React 中，当**计数**改变时，整个组件被重新渲染。*

*当在*跟踪范围*中调用依赖性时，例如在构建“计算”(`createEffect`、`createMemo`等)的 JSX 表达式或 API 调用中，这种依赖性的自动跟踪起作用。)*

> ***跟踪范围:**这些是 SolidJS 源代码中的特定块，当信号的值改变时，信号的值将在这些块中更新。createEffect 是一个跟踪作用域，组件中的 JSX 是一个跟踪作用域，所以在 JSX 使用的任何信号在它改变值时都会被更新。*

*例如，日志记录*(console . log)*count 的值将只运行一次，即使 count 被更新也不会再次运行。*

```
*function Counter() {
  const [count, setCount] = createSignal(1);
  setInterval(() => setCount(count() + 1), 1000);

  console.log(count()); // This will only run when the component firsts renders

  return (
    <div>
      {count()} // This will update when count changes value
    </div>
  );
}*
```

*为了使`console.log`在每次计数更新时运行，它必须在*跟踪范围内(在 JSX 元素中用括号括起来，或者在效果和备忘录 API 中使用)*，如下所示:*

```
*createEffect(() => {
    console.log(count()); // This will run everytime count is updated
  })*
```

****创建信号时完成样本代码****

```
*import { render } from "solid-js/web";
import { createSignal } from "solid-js";

function Counter() {
  const [count, setCount] = createSignal(1);

  setInterval(() => setCount(count() + 1), 1000);

  return <div>Count: {count()}</div>;
}

render(() => <Counter />, document.getElementById('app'));*
```

## *效果*

*像 ReactJS 中的 *useEffect* 一样，效果是包装我们信号的 getter 函数的函数，并且每当依赖信号的值改变时重新执行。这对于创建副作用很有用，比如渲染。*

*可以通过从`solid-js`导入`createEffect`并为其提供一个函数来创建一个效果。效果**自动**订阅功能执行期间读取的任何信号，并在任何信号发生变化时重新运行。*

```
*createEffect(() => console.log("The latest count is", count()));*
```

*使用上面的代码，我们创建了一个*效果*，每当`count`改变时，它就会重新运行。*

*与 React 不同，您不需要指定效果的从属对象。Solid JS 自动检测效果中直接或间接使用的每个**信号**，并为效果订阅信号更新。*

****注:*** *你可以想象 JSX 的每一个表情都自动被一个效果包围，每当它的依赖信号发生变化时，这个效果就会重新执行。这就是为什么 JSX 也是一个* ***可追踪范围*** *。**

****📝我再提醒你一下:*** *当你在 JSX 访问一个* ***信号*** *时，它会自动更新视图当那个* ***信号*** *发生变化时。但是组件函数本身只执行一次。**

## *衍生信号*

*通过将信号包装在函数中，我们可以创建依赖于信号的新表达式。访问信号的函数实际上也是一个信号:当其包装的信号改变时，它将依次更新其读取器。我的意思是:*

```
*const doubleCount = () => count() * 2; 
// doubleCount is a derived signal*
```

*然后，我们可以像 JSX 中的信号一样呼叫`doubleCount`:*

```
*return <div>Count: {doubleCount()}</div>;*
```

*我们称这些函数为 ***衍生信号*** ，因为它们从其访问的信号中获得反应。它们本身并不存储一个值(如果你创建了一个派生信号，但从未调用它，它将像任何未使用的函数一样从 Solid 的输出中被剥离)，但它们将更新任何依赖于它们的效果，并且它们将触发一个重新渲染**(不是字面上的，固体方式)**(如果包含在视图中)。*

## *备忘录*

*备忘录是缓存的派生值。它们共享信号(*只读*)和效果(*观察者*)的属性。它们跟踪自己的相关信号，只有当这些信号发生变化时才重新执行，它们本身就是可跟踪的信号。*

```
*const fullName = createMemo(() => `${firstName()} ${lastName()}`);*
```

*我们可以使用备忘录来评估一个函数并存储结果，直到它的依赖关系改变。这对于缓存具有其他依赖关系的效果的计算和减轻代价高昂的操作(如 DOM 节点创建)所需的工作非常有用。*

*创建备忘录就像传递一个从`solid-js`导入的函数给`createMemo`一样简单。*

*在下面的例子中，重新计算 ***fib()*** 的值随着每次点击变得越来越昂贵，因为它在 JSX 中被调用 **50 次**。*

```
*import { render } from 'solid-js/web';
import { createSignal, createMemo } from 'solid-js';

function fibonacci(num) {
  if (num <= 1) return 1;

  return fibonacci(num - 1) + fibonacci(num - 2);
}

function Counter() {
  const [count, setCount] = createSignal(10);
  const fib = () => fibonacci(count());

  return (
    <>
      <button onClick={() => setCount(count() + 1)}>Count: {count()}</button>

      <div>1\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>2\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>3\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>4\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>5\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>6\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>7\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>8\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>9\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
      <div>10\. {fib()} {fib()} {fib()} {fib()} {fib()}</div>
    </>
  );
}

render(() => <Counter />, document.getElementById('app'))*
```

*如果我们将 **fib(count())** 包装在`createMemo`中，它每次点击只重新计算一次，例如当 **count()** 为 10 时， **fib(count())** 即 **fib(10)** 将在第一次调用时缓存其值，任何其他对 **fib(10)** 的调用将再次使用已经计算的值，而不是再次重新计算。在上面的例子中，createMemo 为我们节省了 49 次重新计算。*

```
*const fib = createMemo(() => {
    // The console.log is added to help monitor how many times the function is called
    console.log('Calculating Fibonacci');
    return fibonacci(count());
  });*
```

# *控制固体中的流动*

*如果，我之前没有声明，SOLID 不像 React 一样使用虚拟 DOM。因此，天真地使用像`Array.prototype.map`这样的东西会浪费地在每次更新时重新创建所有的 DOM 节点。对于一个简单的文本节点，也许这不是问题，但是对于一个越来越大的组件，这是一个问题。*

*Solid 附带了用于包装组件的模板助手，以便于控制流，如条件渲染、循环等。*

## *`**<Show /> Component**`*

***处理三元组(** `**a ? b : c**` **)和布尔表达式(** `**a && b**` **)** ，实为我们提供了`**<Show />**`分量。*

```
*<Show
  when={loggedIn()}
  fallback={<button onClick={toggle}>Log in</button>}
>
  <button onClick={toggle}>Log out</button>
</Show>*
```

*`**fallback**`道具充当`else`并在`**when**`中的条件不正确时显示。*

## *`**<For />**` 组件*

***为了处理对象数组的循环，** SOLID 为我们提供了`**<For />**`组件。*

```
*<For each={cats()}>
  {(cat, i) =>
  <li>
    <a target="_blank" href={`https://www.youtube.com/watch?v=${cat.id}`}>
      {i() + 1}: {cat.name}
    </a>
  </li>
  }
</For>

// Note how we referenced i as i(), its a signal
// The array element is not a signal*
```

*在`<For>`组件上有一个道具:`each`，在这里传递数组进行循环。*

*然后，不是直接在`**<For>**`和`**</For>**`之间编写节点，而是传递一个 ***回调*** ，它应该返回一个要呈现的节点..这是一个类似于 JavaScript 的`[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#parameters)` [回调](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#parameters)的函数。*

***注意**该指数是一个*信号*，不是一个常数。这是因为`**<For>**`是*“由引用键控”*:它呈现的每个节点都耦合到数组中的一个元素。换句话说，如果一个元素改变了在数组中的位置，而不是被销毁和重新创建，那么相应的节点也会移动，其索引也会改变。*

```
*import { render } from 'solid-js/web';
import { createSignal, For } from 'solid-js';

function App() {
  const [cats, setCats] = createSignal([
    { id: 'z_AbfPXTKms', name: 'Maru' },
    { id: 'J---aiyznGQ', name: 'Keyboard Cat' },
    { id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
  ]);

  return (
    <ul>
      <For each={cats()}>{(cat, i) =>
        <li>
          <a target="_blank" href={`https://www.youtube.com/watch?v=${cat.id}`}>
            {i() + 1}: {cat.name}
          </a>
        </li>
      }</For>
    </ul>
  );
}

render(() => <App />, document.getElementById('app'))*
```

*🗒 ***注:*** *如果你的阵是静态的，用阵图也不错。**

## *`**<Index>**`组件**组件***

*与`<For>`有相似的签名，e*x 除了这次* ***项*** *是信号，索引是固定的*。每个渲染节点对应于数组中的一个点。每当该点的数据发生变化，信号就会更新。*

```
*<Index each={cats()}>{(cat, i) =>
  <li>
    <a target="_blank" href={`https://www.youtube.com/watch?v=${cat().id}`}>
      {i + 1}: {cat().name}
    </a>
  </li>
}</Index>

// Note how we referenced cat as cat(), its a signal
// i is not a signal here*
```

*`<For>`和`<Index>`每个渲染节点都带有一个数组元素，所以当一个数组元素改变时，只有对应的节点会重新渲染。*

***不同之处在于当数组元素改变时 DOM 如何更新。***

*`<Index>`会按索引做这个*:每个节点对应数组中的一个索引；`<For>`会这样做*按值*:每个节点对应数组中的一段数据。这就是为什么在回调中，`<Index>`给你一个项目的信号:每个项目的索引被认为是固定的，但是在那个索引上的数据可以改变。另一方面，`<For>`为索引提供了一个信号:该项的内容被认为是固定的，但是如果数组中的元素被移动，它可以移动。**

*`*<For>*` *关心你数组中的每一条数据，并且那些数据的位置可以改变；* `*<Index>*` *关心你数组中的每个索引，每个索引处的内容可以变化。**

## *`**<Switch>**` **和** `**<Match>**` **分量***

*我们经常处理具有多个独立结果的条件句，模仿 Javascript 的`switch` / `case`的`<Switch>`和`<Match>`组件可以在这种情况下派上用场。*

*让我们用`<Switch>`替换这个`<Show>`组件*

```
*<Show
      when={x() > 10}
      fallback={
        <Show
          when={5 > x()}
          fallback={<p>{x()} is between 5 and 10</p>}
        >
          <p>{x()} is less than 5</p>
        </Show>
      }
    >
      <p>{x()} is greater than 10</p>
</Show>

// Feels like callback hell 😃*
```

*使用`<Switch>`的更优雅的解决方案*

```
*<Switch fallback={<p>{x()} is between 5 and 10</p>}>
  <Match when={x() > 10}>
    <p>{x()} is greater than 10</p>
  </Match>
  <Match when={5 > x()}>
    <p>{x()} is less than 5</p>
  </Match>
</Switch>*
```

## *`**<Dynamic>**` **组件***

*这在呈现表单数据时非常有用。它允许您传递一个本地元素的字符串或一个组件函数，并且它将使用提供的其他属性来呈现它。*

*下面用样例代码来理解一下吧；*

```
*import { render, Dynamic } from "solid-js/web";
import { createSignal, Switch, Match, For } from "solid-js";

const RedThing = () => <strong style="color: red">Red Thing</strong>;
const GreenThing = () => <strong style="color: green">Green Thing</strong>;
const BlueThing = () => <strong style="color: blue">Blue Thing</strong>;

const options = {
  red: RedThing,
  green: GreenThing,
  blue: BlueThing
}

function App() {
  const [selected, setSelected] = createSignal("red");

  return (
    <>
      <select value={selected()} onInput={e => setSelected(e.currentTarget.value)}>
        <For each={Object.keys(options)}>{
          color => <option value={color}>{color}</option>
        }</For>
      </select>
      {// To be replaced with Dynamic tag}
      <Switch fallback={<BlueThing />}>
        <Match when={selected() === "red"} ><RedThing /></Match>
        <Match when={selected() === "green"}><GreenThing /></Match>
      </Switch>
    </>
  );
}

render(() => <App />, document.getElementById("app"));*
```

*这段代码运行良好。但是使用`<Dynamic>`组件可以使其更加紧凑。**请注意上面代码中的选项对象。***

*在上面的例子中，我们可以替换`<Switch>`语句:*

```
*<Switch fallback={<BlueThing />}>
  <Match when={selected() === 'red'}><RedThing /></Match>
  <Match when={selected() === 'green'}><GreenThing /></Match>
</Switch>*
```

*使用:*

```
*<Dynamic component={options[selected()]} />*
```

## *`**<Portal>**`组件**组件***

*Solid 有一个`<Portal>`组件，它的子内容将被插入到您选择的位置。*默认情况下，其元素会呈现在*`*<div>*`*`*document.body*`*中。***

```
**<Portal>
  <div class="popup">
    <h1>Popup</h1>
    <p>Some text you might need for something or other.</p>
  </div>
</Portal>**
```

**`useShadow`将元素放在阴影根中进行样式隔离，如果插入到 SVG 元素中则需要`isSVG`，这样就不会插入`<div>`。**

## **<errorboundary>组件</errorboundary>**

**源于 UI 的 JavaScript 错误不应该破坏整个应用程序。错误边界是捕捉子组件树中任何位置的 JavaScript 错误、记录这些错误并显示一个后备 UI 而不是崩溃的组件树的组件。**

```
**<ErrorBoundary fallback={err => err}>
  <Broken />
</ErrorBoundary>**
```

**示例源代码:**

```
**import { render } from "solid-js/web";
import { ErrorBoundary } from "solid-js";

const Broken = (props) => {
  throw new Error("Oh No");
  return <>Never Getting Here</>
}

function App() {
  return (
    <>
      <div>Before</div>
      <ErrorBoundary fallback={err => err}>
        <Broken />
      </ErrorBoundary>
      <div>After</div>
    </>
  );
}

render(() => <App />, document.getElementById("app"));**
```

**通过以上的讨论，我相信你已经可以看到 SOLIDJS 是多么的可爱和有用。还有更多要谈的，生命周期，绑定，存储，甚至用 SOLIDJS 读取数据。**

**一定要拍下这篇文章，关注我的进一步更新。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*******

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***