# 你应该对所有事情都使用 JavaScript 吗？

> 原文：<https://javascript.plainenglish.io/should-you-use-javascript-for-everything-f98015ade40a?source=collection_archive---------12----------------------->

## 根据您的开发需求权衡使用 JavaScript 的利弊。

![](img/f6b9c981634d1230b38152e82db1d762.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

围绕 JavaScript 的工具和技术不同于任何其他语言。使用各种开源框架和库，你可以创建任何东西，从全功能的桌面应用到像 API 这样的服务器应用。但是即使这些技术对我们来说是可用的，我们应该使用它们吗？让我们探索一些不同的用例，并权衡使用 JavaScript 和另一种方法的利弊。

# **网页开发**

![](img/92b23c69b6faea3b2ce227793dd6a851.png)

Photo by [Farzad Nazifi](https://unsplash.com/@euwars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 开发的核心部分，根据 [w3techs](https://w3techs.com/technologies/details/cp-javascript/) 的数据，大约 97.8%的网站在编写时(2022 年 2 月)使用客户端 JavaScript。这并不奇怪，因为大多数网站都使用分析工具、客户端路由和更多基于 JavaScript 的概念。

现在，当涉及到开发一个网站，很可能你将需要应用这些概念来改善网站。然而，有些网站或网站的某些部分使用其他东西可能会更好。如果你的网站正在执行任何复杂的操作，你可能会更喜欢像 [WASM](https://en.wikipedia.org/wiki/WebAssembly) 这样的东西，因为它可以将各种高性能语言的代码编译成标准化的二进制格式。这用于需要复杂的图形或计算任务(如计算数据和输出到图形)的站点。

另一个需要注意的是，JavaScript 经常被用在不需要的地方。例如，您可以使用 JavaScript 通过修改 SVG 的值来创建一个复杂的进入动画，您可以使用一些 CSS 来重新创建它，或者使用 JavaScript 从一个可以在服务器端预呈现的数据库中加载内容。没有一种方法在所有情况下都更好，但是最好考虑一下在客户端使用 JavaScript 的原因。

# **桌面&移动应用**

![](img/0ea5d963dab03926e4fd9d26a3ddc608.png)

Photo by [Tran Mau Tri Tam](https://unsplash.com/@tranmautritam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用像 Electron、Tauri、React-Native 或其他工具这样的框架，开发人员可以毫不费力地将 web 应用打包成桌面应用。它们通常还提供对特定于设备的 API 的访问，这些 API 由于隐私或安全原因还没有被 web 实现或拒绝。这些通常可以编译到多个平台上，并根据框架的设计方式而有不同的包大小。

这使得开发人员不仅可以轻松地发布到 web 上，还可以在一个代码库中发布到桌面和移动平台上。然而，缺点也不是微不足道的。这些框架历来臃肿和/或性能低下。这种情况正在改变，特别是在桌面领域，像 Tauri 这样的人正在编译时构建东西，但它只是最近才进入发布候选空间，还有很长的路要走。

这些系统的替代物是像 Flutter 或 QT 这样的 C++框架，它们是用编译语言创建的，是跨平台的。但这只有在你能为这些平台贡献一个团队的情况下才有意义。虽然 Flutter 确实发布到了网络上，但这并不是最好的体验，你可能需要一个单独的代码库。然而，Flutter 是基于 Dart 构建的，Dart 非常类似于 TypeScript。这使得它更容易学习，但它仍然是一个障碍，可能会使你选择基于 web 的框架而不是 Flutter。

# **服务器应用**

![](img/31d693bbc58c6fa11bdbf30715077d40.png)

Photo by [Florian Krumm](https://unsplash.com/@floriankrumm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是一个非常常见的 JavaScript 运行时，用于使用 Express 和 Nest 等框架创建服务器端应用程序。这不是唯一的一个，Deno 正在运行时领域崭露头角。

许多服务器端应用程序都是内置的 Node.js，因为它很快，而且一般来说，你可以让相同的人在前端和后端工作，如果他们已经知道相关的语言，这将很有帮助。但是如果你需要你的服务器快如闪电的话，这并不好。这对于 99%的项目来说都没问题，因为您总是可以在多台机器之间实现负载平衡，但是如果您需要一个响应速度高于平均水平的高性能服务器，比如在时间敏感的场景中(例如股票市场)，您可能希望选择编译语言。

# **嵌入式系统&物联网**

![](img/3f536e309f7794c09a710be59d9e5e93.png)

Photo by [BENCE BOROS](https://unsplash.com/@benceboros?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这些技术在尺寸和功率上都有很大的差异。也许汽车的触摸屏甚至手持扫描仪使用 WebView 显示信息，并使用 JavaScript 使 WebView 具有交互性。我找不到这篇文章，但我记得 Svelte 的创始人提到过，Svelte 已经被用于像这样的小型设备中，以消除虚拟 DOM 所需的计算。他们本可以使用传统技术创建一个应用程序，但决定利用 JavaScript 等 web 技术的力量来使开发变得快速而简单。

# 结论

无论您是否使用 JavaScript，都需要理解其中的利弊。如果您的团队已经熟悉这些技术，JavaScript 可能会减少开发时间，但可能会导致性能折衷，反之亦然。性能的权衡通常不是什么大问题，但是如果您在严格的限制下工作，或者要执行复杂的计算，那么就有必要问问 JavaScript 是否是您的正确解决方案。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*