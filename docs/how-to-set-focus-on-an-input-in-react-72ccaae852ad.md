# 如何在 React 中将焦点设置在输入上

> 原文：<https://javascript.plainenglish.io/how-to-set-focus-on-an-input-in-react-72ccaae852ad?source=collection_archive---------0----------------------->

## 通过自动将焦点应用于输入来改善用户体验

![](img/9395eb65737ee5e9a2a404e4270696a9.png)

React Logo courtesy of React

要在 React 中将焦点设置在输入上:

1.  在输入元素上设置参考
2.  对 ref 元素调用 focus()方法

## 在单击按钮时设置输入焦点

```
*import* {useRef} *from* ‘react’;function App() {const inputRef = useRef(null);*return* (<div ><input *ref*={inputRef}/><button *onClick*={() => {inputRef.current.focus()}}>Focus input</button></div>);}*export* *default* App;
```

在上面的代码中，您创建了对输入字段(inputRef)的引用，并且在按下按钮时，您引用了 inputRef 并对其运行了 focus 方法。

## 按 enter 键时将焦点设置在输入上

当用户在一个输入中单击 enter 时，您可能希望将他们移到下一个输入中。为此，您需要创建一个每当用户在输入中按下一个键时运行的方法。如果键码是回车键的键码，那么您可以将焦点转移到下一个输入。

```
*import* {useRef} *from* ‘react’;function App() {const inputRef = useRef(null);const inputRefTwo = useRef(null);function checkPress(e){*if*(e.keyCode == 13){inputRefTwo.current.focus();}}*return* (<div ><input *ref*={inputRef} *onKeyPress*={(e) => checkPress(e)}/><input *ref*={inputRefTwo}/></div>);}*export* *default* App;
```

## **在页面加载时设置输入焦点**

通过使用 HTML 自动聚焦属性，可以在页面为用户加载时聚焦输入，这是最简洁的方法。或者，当使用 useEffect 钩子加载页面时，可以聚焦一个引用，尽管这需要更多的代码来实现

```
function App() {*return* (<div ><input *autoFocus*/></div>);}*export* *default* App;
```

希望本教程能帮助你在各种场景中自动聚焦输入！自动将焦点应用于输入可以显著改善用户体验，使用户更快地向应用程序提供信息。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****