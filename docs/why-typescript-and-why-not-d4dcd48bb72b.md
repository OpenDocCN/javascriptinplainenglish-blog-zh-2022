# 为什么是 TypeScript，为什么不是？

> 原文：<https://javascript.plainenglish.io/why-typescript-and-why-not-d4dcd48bb72b?source=collection_archive---------16----------------------->

## 了解 TypeScript 如何为您带来好处

2022 年还有 JavaScript 开发者对 TypeScript 不太确定或者没听说过。

![](img/7128ac13c347ee92c3608dd1f95c7818.png)

Screenshot from [2020 StateOfJS](https://2020.stateofjs.com/en-US/technologies/)

TypeScript 的接受度越来越高，开发人员对此很满意。当然也不能盲目跟风。

# 什么是 TypeScript？

TypeScript 是一种基于 JavaScript 的强类型编程语言，由微软开发和维护。它是 JavaScript 的一种严格语法，并为语言添加了可选的静态类型。TypeScript 是为开发大型应用程序而设计的，可以编译成 JavaScript。

# 为什么要用 TypeScript 而不是 JavaScript？

## 静态打字

大多数开发人员使用 typescript，因为它提供静态类型。JavaScript 是一种非常脆弱的编程语言，因为它的动态类型特性。

当您在开发过程中遇到类型错误时，所有的代码编辑器都会向您抛出警告或错误。我将在 Vue 中展示一个例子。

`e`是一个[事件](https://developer.mozilla.org/en-US/docs/Web/API/Event)，IDE 不会帮你自动完成，也不会给你看它有什么方法；要么使用`JSDoc`要么查看文档。但是，除非你明确声明，否则你无法判断它是一个`InputEvent`还是`MouseEvent`。

另一种情况是，有时值为 [nullish](https://developer.mozilla.org/en-US/docs/Glossary/Nullish) 。如果没有 IDE/TypeScript 的帮助，您可能会遇到运行时错误。例如:

```
const body = document.querySelector(".foo") // null
body.classList.add("bar"); // no error and crash during runtime
```

如果上面的代码是用 TypeScript 编写的，在开发或编译过程中你会得到一个错误`TS2531: Object is possibly ‘null’.`。

## 生产力

想象你正在集成 API 并在你的前端显示它。您总是需要检查响应或文档，有时您可能会忽略或输入错误，您将不会在 JavaScript 中得到任何错误。

您可以使用一些工具将 JSON 响应转换为 TypeScript 的类型，如在线工具 [JSON to TypeScript](https://quicktype.io/typescript) 。IDE 将自动完成并显示 API 响应体的内容。你不必浪费时间手动检查或记忆身体。

# 什么时候不使用 TypeScript？

你不喜欢静态打字。你相信你自己和你的队友`TypeError`不会或很少在运行时发生。

您正在进行一个小项目`~100 lines of codes`，这对于设置一个 TypeScript 环境来说是没有意义的。

你盲目地追随 TypeScript 潮流，对此一无所知或知之甚少，将所有类型都声明为`any`

你是一个懒于声明类型的人，在`tsconfig.json`中关闭选项`noImplicitAny`，或者在任何地方放置`@ts-ignore`。

你可以记住所有的 API 响应体，没有一个错别字。

如果您是一名经验丰富的 TypeScript 开发人员，请务必查看我的文章，了解高级用法

[](https://betterprogramming.pub/7-advanced-usages-of-typescript-f9abb0dd64ff) [## TypeScript 的 7 种高级用法

### 您是否编写了大量冗余类型的代码？以下是一些高级功能。

better 编程. pub](https://betterprogramming.pub/7-advanced-usages-of-typescript-f9abb0dd64ff) 

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*