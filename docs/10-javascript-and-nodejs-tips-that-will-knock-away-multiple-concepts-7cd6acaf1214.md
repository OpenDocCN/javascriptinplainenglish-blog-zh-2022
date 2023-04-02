# 消除多个概念的 10 个 JavaScript 和 Node.js 技巧

> 原文：<https://javascript.plainenglish.io/10-javascript-and-nodejs-tips-that-will-knock-away-multiple-concepts-7cd6acaf1214?source=collection_archive---------5----------------------->

## 轻松消除多个概念的 JavaScript 和 Node.js 顶级技巧。

![](img/a50c5bb12ee09e6e8136c20a7801954f.png)

Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages) on Unsplash

当我前几天查看 JavaScript 中的一些对象时，我意识到选择*学习什么*是在学习过程中取得巨大进步的有效方法。在今天的世界里，如果你想赚钱，聪明地工作是一条出路。这是因为价值是赚钱的机器。某样东西对某人来说越有价值，这个人为它付钱的机会就会大大增加。

当我回顾我的起步阶段时，我很感激在我职业生涯的很早就学会了`forEach`、`map`、`filter`和`reduce`、*，因为我*开始在任何地方都能看到它们*。我当时并不知道，但首先学习它们是明智之举。我的意思不是仅仅看一些关于如何使用它们的文档。我读了深入研究这些话题的书。*

学习像`reduce`这样的东西和学习像`map`这样的东西是有区别的。如果有人问我，我想先学哪一门，以后再学哪一门。我会选择`reduce`开始，因为掌握`reduce`已经可以帮助我同时熟悉`filter`和`map`*，因为它可以在同一个功能块中完成这两个功能:*

*这篇文章将介绍 10 个 JavaScript 和 NodeJS 技巧，每个技巧都能一石激起千层浪*

# *请求对象(提示:`window.fetch`)*

*开发 web 应用程序时，在 JavaScript 中使用过 [window.fetch](https://developer.mozilla.org/en-US/docs/Web/API/fetch) API 吗？这个热门功能有两个我推荐尽快学习*的黄金对象*。*

*我现在看到的问题是，当文章谈到 fetch API 时，并没有真正讨论这些对象。当然有些人会说通过访问`body`属性和头来读取响应数据，但是即使知道响应数据的不同*数据类型*也会大有帮助。[请求](https://developer.mozilla.org/en-US/docs/Web/API/Request)和[响应](https://developer.mozilla.org/en-US/docs/Web/API/Response)对象被*包裹在你发出的每一个请求*中。*

*当您学习 *Request* 接口时，您实际上是一石多鸟，因为当您尝试使用 JavaScript 社区可用的第三方工具时，您会意识到这个接口是有意模仿的，以简化(*和* unify)所有使用 HTTP 请求/响应管道的应用程序开发。*

*例如，我使用 Gatsby 函数，它们传递给每个函数的参数包括[请求](https://www.gatsbyjs.com/docs/reference/functions/getting-started/#introduction)对象，该对象与 Node.js 中 HTTP 模块的对象[相同。](https://nodejs.org/api/http.html#http_class_http_incomingmessage)*

*再比如 JavaScript 中的 [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 。Workers 是现代 web 应用程序中的一个热门特性，它也使用了`fetch` API，其中再次出现了`Request`对象。*

# *响应对象(提示:`window.fetch`)*

*就像*请求*对象一样，*响应*对象与*请求*对象一样重要(如果不是更重要的话)，因为它包含了应用程序中最敏感的部分——响应*数据*。*

*一旦您熟悉了请求和响应接口，您将更容易理解第三方工具的文档。*

*例如，像 GatsbyJS 这样的现代框架(再次)在 Gatsby 函数中模仿了这种结构。ExpressJS 完全是关于处理请求对象和响应对象的，这些对象被雅虎、亚马逊、LinkedIn、纽约时报、家得宝、AT、Meetup、华尔街日报、Docker 等知名公司所使用(来源: [stackshare](https://stackshare.io/feed) )。*

*我通过[@ AWS-SDK/client-Lambda](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-lambda/classes/lambda.html)SDK 使用 AWS Lambda 函数，并在将`InvocationType`设置为`"RequestResponse"`时看到具有相同`body`、`headers`、`statusCode`属性的类似请求/响应对象*

*我还使用了 Netlify 函数，您必须从每个处理程序返回的对象与您从带有 statusCode 的`Response`中看到的形状相同，您必须知道 status code 才能确保消费者相应地处理它。*

# *咖喱功能*

*JavaScript 中的 Curry 函数是一次接受一个或多个参数并返回一个期望下一个(或剩余)参数的新函数的函数。这是一个函数转换，它返回新的函数，直到所有的参数都完成为止。*

*如果你是编程初学者，这可能听起来很奇怪。你很可能会问自己，为什么有人会通过给出函数来返回函数。这是现实世界中不同的概念。如果我们想要苹果，我们不想必须付出苹果才能得到苹果。为什么不直接给出函数，马上得到我们需要的东西呢？*

*currying 提供的好处使得像 [lodash](https://lodash.com/docs/4.17.15) 这样的库如此强大。您可以创建一个预定义了一些行为的函数，然后将其作为即将到来的值的转换来重用(提示:在 JavaScript 中，即使是*函数也被视为值*)。lodash-fp 在他们所有的代码中都使用这种模式，并帮助你使用一种全新的编程范式。*

*理解 currying 就是理解*功能组成*。当你花大量时间想出优雅的方法来组合函数时，你已经在一步到位地使用高级概念了，比如词法范围、闭包、高阶函数(下一节)、执行上下文、正确传递`this`(如果依赖的话)、维护引用等等。*

*我的意思是:*

*以下是该代码片段中作为执行 currying 的结果而发生的所有事情:*

1.  *高阶函数*
2.  *词法范围*
3.  *关闭*
4.  *维护参考*
5.  *部分应用*
6.  *维护`this`(如果你愿意的话)*
7.  *隐藏实现细节*
8.  *将同一个对象共享给所有将来要使用的函数*

*充分利用这种技术的一个很好的例子是来自 [redux](https://github.com/reduxjs/redux) 库中的 [createStore](https://github.com/reduxjs/redux/blob/master/src/createStore.ts) 函数。(提示:该代码片段中有一些注释描述了函数执行时的一些简洁行为)*

# *高阶函数*

*我们之前讨论过 curry 函数的好处。我们也很少提到*高阶函数*。*

*通过学习 currying，您还可以学习如何实际操作高阶函数，这是 JavaScript 中的另一个重要概念，可以让您的学习过程有一个大的飞跃。*

*当你学习高阶函数时，你也在学习:*

1.  *如何使用以及如何*可视化*闭包*
2.  *如何创建部分应用程序功能*
3.  *变量是如何记忆的(这可能有助于你理解记忆)*

*几乎所有的 JavaScript 库都支持高阶函数。最重要的是你能用高阶函数做什么。如果你能理解高阶函数，你就已经开始理解如何使用高级技术，比如 JavaScript 中的[转换器](https://stackoverflow.com/questions/52274362/is-my-understanding-of-transducers-correct)。*

# *标准输出/标准输入/标准错误*

*如果你喜欢在 NodeJS 上开发应用程序(甚至是 web 应用程序)，学习/使用`stdout`、`stderr`和`stdio`可能是必须的。直到后来在我的开发生涯中，我才注意到这一点。*

*我一点也不知道我几乎在[的每一个文件](https://nodejs.org/dist/latest-v17.x/docs/api/console.html#new-consolestdout-stderr-ignoreerrors)中与`stdout`一起工作。*

*理解`stdout`、`stderr`和`stdio`以及它们是如何在应用程序中突然被使用的，使得我不久前开始关注它的时候，很多神奇框架中的概念在我脑海中“咔嚓”一声闪现。*

*不久前，我还打算学习 Node.js 中的本机`child_process`模块是如何工作的，但我一直把它放在一边。当我最终决定亲自动手时，我意识到`stdout`已经揭开了我对这个模块的神秘面纱。然后我就很容易进入像 [Ink](https://github.com/vadimdemedes/ink) 这样的工具。*

# *承诺(结合回拨概念)*

*掌握承诺和回调将提高您使用异步代码的能力。回调和承诺*也无处不在*。*

*如果你是初学者，这应该是首先要掌握的事情之一。在处理复杂代码时，你的调试能力也会提高，比如面试中经常出现的这段烦人的代码片段:*

# *虚拟思维*

*毫无疑问:用虚拟数据结构思考是现代应用程序开发的必由之路。这是一个在 [React](https://reactjs.org/) 中流行的概念，它启发了像 [virtual-dom](https://www.npmjs.com/package/virtual-dom) 这样的库为 web 应用程序提供更多编写高性能代码的方法。*

*当您开始理解使用虚拟数据结构的好处以及为什么使用虚拟数据结构比直接使用 DOM 更好时，您就已经理解了驱动当今许多 web 应用程序的现代技术的一半了。这种技术的一些例子是[再水合](https://github.com/rt2zz/redux-persist)和[服务器组件](https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html)。*

*见鬼，在虚拟结构中思考甚至会帮助你的速度和能力直接处理 [AST](https://babeljs.io/docs/en/babel-types) 结构。最终，你的大脑只是在简单的物体上锻炼了这么多。*

# *遍历/使用 DOM*

*正确地遍历 DOM(按照预期的顺序正确地访问孩子/父母)将有助于您理解几件事情:*

1.  *如何使用 ASTs(当您能够轻松使用 ASTs 时，您就能够轻松地创建自己的 babel 插件和/或使用 TypeScript 之类的工具进行编程)*
2.  *如何理解 ASTs*
3.  *树遍历(您自动理解遍历树以及如何以可预测的方式收集结果)。不要太害怕像“深度优先搜索”或“二分搜索法”这样可怕的词，只要想想当你遍历一个 DOM 的后代或祖先时你在 DOM 中做了什么。当你初来乍到，有人告诉你开始理解面试中的树遍历时，你可能会感到不知所措，因为你甚至不知道从哪里开始。从 DOM 开始。不要想太多。*
4.  *像 MDX 这样的现代工具是如何在表面下工作的。*

# *传播事物*

*当你花大量时间传播这些东西时，你可以学到一些非常重要的概念:*

*通过反复试验，你最终会遇到错误，你会想:*

1.  *为什么有些对象没有扩散反而导致错误(提示:`{ ...options.bar }`如果 options.bar 不是对象怎么办？)*
2.  *为什么有些数组没有展开反而导致错误(提示:`[...options.bar]`如果 options.bar 不是数组怎么办？)*
3.  *为什么`undefined`会“扩散”到对象中，而`null`不会*
4.  *如何“使”一个对象“可扩展”(提示:[可迭代协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)，换句话说，与`[Symbol.iterator]`一起工作)。这将有助于你理解上述所有概念*

*这里值得注意的是，您可能还想了解合并对象的另一种方式(`Object.assign`)会产生副作用:*

*结果(`myFruits`变了):*

# *一滴*

*斑点到处都是。它们可以在`window.fetch`中找到，序列化为`img`和`video`的 URL，上传文件，作为某些响应的数据类型返回，等等。*

*熟悉如何使用`Blob`。这是用于在线媒体共享(例如图像和视频)、流式传输、跨网络分发文件、存储日志文件并更新它们、文件恢复、数据存储(例如分析应用)以及物联网(物联网)应用的对象。*

# *结论*

*本帖到此结束！我希望你已经在这里找到了有价值的信息，并期待在未来从我这里得到更多！*

**更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****