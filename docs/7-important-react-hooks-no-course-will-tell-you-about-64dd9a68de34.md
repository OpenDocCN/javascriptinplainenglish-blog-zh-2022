# 没有课程会告诉你的 7 个重要反应

> 原文：<https://javascript.plainenglish.io/7-important-react-hooks-no-course-will-tell-you-about-64dd9a68de34?source=collection_archive---------1----------------------->

## #3 是游戏规则的改变者。

![](img/c63b65472bbee7056590dd166f66b481.png)

Photo by [Grzegorz Walczak](https://unsplash.com/@grzegorzwalczak?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在线课程改变了网络开发的场景。

我认识的大部分开发人员都是从一门免费或付费的课程中学到 web 开发的。

这些课程倾向于提供最新的指南和最佳实践，通常是面向绝对的初学者。

因为它们是为初学者设计的，所以它们必须在一门课程中涵盖很多内容，同时确保这门课程不会过于庞大。

向每一个课程创造者致敬——我非常感谢你们分享你们的技能并教育大众！

大多数开发人员一行一行地遵循课程，并按照课程中显示的那样构建项目，他们从来不会对此进行第二次思考。

这些课程没有涵盖所有的基本细节，因为这将使课程对目标受众产生威胁，并可能影响他们的收入。

虽然这听起来不错，但是一旦你开始构建多个项目(尤其是当你构建一个投资组合或者自由职业者的时候)，你会想要一个更快的方法来构建一些公共功能。

幸运的是，使用 React hooks，您只需几行代码就可以添加一些最常见的方法和特性，而且不会影响可读性。

以下是我整理的 7 个定制挂钩，可以增强你的应用程序:

## #1.[使用悬停](https://usehooks.com/useHover/)

悬停事件是传达信息的重要媒介。

例如，当用户悬停在受限链接上时，您可以显示一个禁用的标志，或者您可以突出显示一个按钮来传达用户光标所在的按钮。

通常，您可以使用如下所示的`onMouseOver` & `onMouseOut`来处理悬停事件(当光标悬停时以及当光标最终离开时):

```
import React from "react";
import "./styles.css";

export default function App() {
   let [over,setOver]=React.useState(false);

   let buttonstyle={
    backgroundColor:''
  }

  if(over){
    buttonstyle.backgroundColor="green";
  }
  else{
    buttonstyle.backgroundColor='';
  }

  return (
    <div className="App">
      <button style={buttonstyle}
      onMouseOver={()=>setOver(true)} 
      onMouseOut={()=>setOver(false)}
      >Hover over me!</button>
    </div>
  );
}
```

所有这些只是为了处理悬停事件。

使用`useHover`，您只需一行代码就可以做到这一点，并在您希望处理悬停事件的组件上设置 ref 属性。

```
// Usage
function App() {
  const [hoverRef, isHovered] = useHover();
  return <div ref={hoverRef}>{isHovered ? "😁" : "☹️"}</div>;
}
```

是不是很酷？

自定义挂钩的代码如下所示。您可以将其复制到一个新文件中，然后在需要悬停挂钩时导入该文件。

```
function useHover() {
  const [value, setValue] = useState(false);
  const ref = useRef(null); const handleMouseOver = () => setValue(true);
  const handleMouseOut = () => setValue(false); useEffect(
    () => {
      const node = ref.current;
      if (node) {
        node.addEventListener("mouseover", handleMouseOver);
        node.addEventListener("mouseout", handleMouseOut);
        return () => {
          node.removeEventListener("mouseover", handleMouseOver);
          node.removeEventListener("mouseout", handleMouseOut);
        };
      }
    },
    [ref.current] // Recall only if ref changes
  );
  return [ref, value];
}
```

**代码解释:**

如你所见，我们使用`useRef()`创建了一个 ref 对象，然后我们添加了事件监听器来监听鼠标悬停和鼠标离开事件，并使用`useEffect()`钩子相应地更新值。

## #2.[使用本地存储](https://usehooks.com/useLocalStorage/)

如果您的应用程序处理大量的表单字段，那么访问您的状态并将其复制到本地存储可以创建一种客户端友好的体验。

当我在构建 [Wildfire](https://usewildfire.com/) 的时候，我必须处理本地存储，这样即使作者在写博客的时候不小心关闭了标签，他的工作也是安全的。

`useLocalStorage`是一个方便的钩子，可以让您轻松地访问和存储本地存储中的值。

```
function App() {
// First arg is key to the value in local storage. const [name, setName] = useLocalStorage("name", "Bob");
  return (
    <div>
      <input
        type="text"
        placeholder="Enter your name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </div>
  );
}
```

这里，“name”是键，默认值是“Bob”。可以用这个代替`useState()`。它提供了类似的功能，同时还增加了本地存储持久性。

挂钩的代码附在下面。

```
import { useState } from "react"; // Hook
function useLocalStorage(key, initialValue) {
  // State to store our value
  // Pass initial state function to useState so logic is only //executed once const [storedValue, setStoredValue] = useState(() => {
    if (typeof window === "undefined") {
      return initialValue;
    }
    try {
      // Get from local storage by key
      const item = window.localStorage.getItem(key);
      // Parse stored json or if none return initialValue
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      // If error also return initialValue
      console.log(error);
      return initialValue;
    }
  }); // Return a wrapped version of useState's setter function that ...
  // ... persists the new value to localStorage.
  const setValue = (value) => {
    try {
      // Allow value to be a function so we have same API as useState
      const valueToStore =
        value instanceof Function ? value(storedValue) : value;
      // Save state
      setStoredValue(valueToStore);
      // Save to local storage
      if (typeof window !== "undefined") {
        window.localStorage.setItem(key, JSON.stringify(valueToStore));
      }
    } catch (error) {
      // A more advanced implementation would handle the error case
      console.log(error);
    }
  }; return [storedValue, setValue];
}
```

**代码解释:**

我们使用`useState()`来管理我们的键值对的状态。如这个钩子的使用代码片段所示，我们接受了两个参数作为键和初始值。

使用这些参数，我们在`useState()`中创建了一个函数，从本地存储中获取数据，如果存在就返回，否则我们将返回初始值。

我们不能直接使用`setStoredValue()`,因为那样只会更新值而不会更新本地存储，因此我们创建了一个新函数`setValue`,它检查窗口是否未定义(也就是说，我们正在浏览器中运行),并使用`setStoredValue()`更新本地存储和值。

## #3.[使用-http](https://github.com/ava/use-http)

这是一个非常棒的钩子，我怎么推荐都不为过。

在构建前端应用程序时，访问 API 是一种常见的用法，但是编写全面的获取代码(也就是说，包括错误处理和重试选项)不仅单调，而且非常令人沮丧。

这个包提供了一种直观的方式来处理你的获取操作

SSR 支持也包括在内。

```
import useFetch from 'use-http'

function Todos() {
  const [todos, setTodos] = useState([])
  const {get, post, response, loading, error} = useFetch('https://example.com',
{
   retries: 1,
    retryOn: [305],
    // OR
    retryOn: async ({ attempt, error, response }) => {
      // returns true or false to determine whether to retry
      return error || response && response.status >= 300
    },

    retryDelay: 3000
});

  useEffect(() => { initializeTodos() }, []) // componentDidMount

  async function initializeTodos() {
    const initialTodos = await get('/todos')
    if (response.ok) setTodos(initialTodos)
  }

  async function addTodo() {
    const newTodo = await post('/todos', { title: 'my new todo' })
    if (response.ok) setTodos([...todos, newTodo])
  }

  return (
    <>
      <button onClick={addTodo}>Add Todo</button>
      {error && 'Error!'}
      {loading && 'Loading...'}
      {todos.map(todo => (
        <div key={todo.id}>{todo.title}</div>
      ))}
    </>
  )
}
```

所有标准操作(GET 和 POST)以及必要的加载和错误状态都可以用`use-http()`轻松处理。

此外，在上面提供的代码片段中，您还可以看到重试逻辑。

我想不出更简单的方法来处理获取操作。

## #4.[使用门户](https://github.com/alex-cory/react-useportal)

顾名思义，如果您没有使用任何 UI 库，并且想要创建门户、工具提示、下拉菜单、全局消息通知和其他类似的项目，那么这个包是非常好的。

就我个人而言，我还没有使用这个包，因为我使用的是 Chakra UI，它为我提供了现成的模态和工具提示，但尽管如此，这个包应该在列表中占有一席之地。

您可以在下面看到使用这个包创建一个带动画的门户有多快:

```
import usePortal from 'react-useportal'

const App = () => {
  const { openPortal, closePortal, isOpen, Portal } = usePortal()
  return (
    <>
      <button onClick={openPortal}>
        Open Portal
      </button>
      <Portal>
        <p className={isOpen ? 'animateIn' : 'animateOut'}>
          This Portal handles its own state.{' '}
          <button onClick={closePortal}>Close me!</button>, hit ESC or
          click outside of me.
        </p>
      </Portal>
    </>
  )
}
```

其他功能，如在外部单击时关闭模态，支持服务器端呈现和类型脚本，都内置在这个包中。

通常，从头开始创建一个门户或模型需要很多代码，这个包非常适合这样的用例。

***如果你喜欢这篇文章并觉得它很有帮助，可以考虑使用*** [***我的推荐链接***](https://medium.com/@anuragkanoria/membership) ***，这样你就可以无限制地访问我的博客以及其他作者的博客，只需点击*** [***这里***](https://medium.com/@anuragkanoria/membership) ***。***

## #5.[反应悬挂器](https://github.com/kitze/react-hanger)

React-hanger 是那些当你开始使用它们的时候，你真正欣赏的工具之一。

这是目前为止我用过的最有效的钩子，我希望我能早点知道。

它是一组有用的钩子，处理基本类型和它们变化的状态。

通过提供助手函数来处理常见的使用模式，它可以极大地简化值的创建和更新。

```
import React, { Component } from 'react';

import { useInput, useBoolean, useNumber, useArray, useOnMount, useOnUnmount } from 'react-hanger';

const App = () => {
  const newTodo = useInput('');
  const showCounter = useBoolean(true);
  const limitedNumber = useNumber(3, { lowerLimit: 0, upperLimit: 5 });
  const counter = useNumber(0);
  const todos = useArray(['hi there', 'sup', 'world']);

  const rotatingNumber = useNumber(0, {
    lowerLimit: 0,
    upperLimit: 4,
    loop: true,
  });

  return (
    <div>
      <button onClick={showCounter.toggle}> toggle counter </button>
      <button onClick={() => counter.increase()}> increase </button>
      {showCounter.value && <span> {counter.value} </span>}
      <button onClick={() => counter.decrease()}> decrease </button>
      <button onClick={todos.clear}> clear todos </button>
      <input type="text" value={newTodo.value} onChange={newTodo.onChange} />
    </div>
  );
};
```

在上面的代码中，您可以看到如何快速切换布尔值，在`newTodo`变量中接受用户输入，以及如何处理数组`todos`。

您还可以在标准原语中获得一些特殊的附加内容，如旋转数(一旦达到上限，它将重置为下限)。

在您的下一个项目中尝试这个包，看看它有多有用。

## #6.[使用媒体](https://github.com/streamich/use-media)

极其直观而强大的软件包。

这个钩子帮助 React 处理 CSS 媒体查询。

给出了处理 CSS 媒体查询改变的标准方式:

```
import React, { useState, useEffect } from 'react';

const App = () => {
  const [matches, setMatches] = useState(
    window.matchMedia("(min-width: 768px)").matches
  )

  useEffect(() => {
    window
    .matchMedia("(min-width: 768px)")
    .addEventListener('change', e => setMatches( e.matches ));
  }, []);

  return (
    <div >
      {matches && (<h1>Big Screen</h1>)}
      {!matches && (<h3>Small Screen</h3>)}
    </div>
  );
}

export default App;
```

然而，有了他的包，它变得相当易读和简单。

```
import useMedia from 'use-media'; const Demo = () => {

  const isWide = useMedia({minWidth: '1000px'});

  return (
    <div>
      Screen is wide: {isWide ? '😃' : '😢'}
    </div>
  );
};
```

这个包也有助于使用上下文跨组件处理[媒体变化。](https://github.com/streamich/use-media#storing-in-context)

## #7.[使用去抖](https://github.com/xnimorz/use-debounce)

![](img/75d386090398563edbfce79f21fd7676.png)

Source: Author

使用自动保存功能？这个包裹是你的救命稻草。

`use-debounce`钩子提供了一种简单的去抖动值的方法。

去抖基本上意味着一个限制调用频率的功能。

在上面的媒体中，您可以看到当实际值更新时，去抖值没有立即更新。反而过一段时间就更新了。

如果你的应用有句子/字数统计或自动保存功能，这个功能就很有用。

```
import { useDebounce } from "use-debounce";function Input() {
  const [text, setText] = useState("Hello");
  const [debouncedText] = useDebounce(text, 1000); return (
    <div>
      <input
        defaultValue={"Hello"}
        onChange={(e) => {
          setText(e.target.value);
        }}
      />
      <p>Actual value: {text}</p>
      <p>Debounced value: {debouncedText}</p>
    </div>
  );
}
```

在上面的代码中，您可以看到使用特定的定时器将去抖添加到任何值是多么容易。

## 最后的想法…

React 让我成为了功能组件及其优势的粉丝。

React hooks 极大地简化了组件生活方式事件，并引入了大量简化构建 web 应用程序的方法。

从上面的列表中，您可以看到 hooks 如何通过让您只关注重要的逻辑来为您的项目增压并帮助您削减开发时间。

希望你喜欢阅读这篇文章。

我定期发表这样的博客，你可以看看我最近在动画图书馆发表的关于 React:

[](/6-animations-library-for-your-next-react-project-9b1d45fcb8e2) [## 为您的下一个 React 项目提供 6 个动画库

### #3 是我现在的最爱之一。

javascript.plainenglish.io](/6-animations-library-for-your-next-react-project-9b1d45fcb8e2) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*