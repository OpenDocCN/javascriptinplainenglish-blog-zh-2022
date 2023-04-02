# 什么是聚合填充和传输填充？

> 原文：<https://javascript.plainenglish.io/what-are-polyfills-and-transpilers-271e4b940e53?source=collection_archive---------5----------------------->

如果您将 JavaScript 代码部署在 web 浏览器上，您可能会在代码中遇到这些单词。polyfill 是一种代码，它在 web 浏览器上实现一种功能，而这种功能不支持像 JS 库这样的功能，它实现 HTML5 或 CSS web 标准或任何 ES6 或 ES7 标准，这些标准对许多浏览器来说可能太新了。

![](img/97af46793f854c0fe9363e365490b26d.png)

虽然您可以通过使用旧的特性实现来管理它，但是如果您真的想使用新的特性，您有两个工具可以使用。

1.  运输工人
2.  多填充物

# 运输工人

翻译程序是一种特殊的软件，它将一个源代码翻译成另一个源代码。它可以解析现代代码，并使用旧的语法结构重写代码，因此它也可以在过时的浏览器中工作。

比如 2020 年之前，JavaScript 没有“可选链接操作符”`?.`。所以，如果你用的是过时的浏览器，它可能无法理解像`height = user?.height`这样的代码。

transpiler 会分析我们的代码并将`user?.height`重写为`(user.height !== undefined && user.height !== null) ? user.height : undefined`。

```
// before running the transpiler
height = user?.height;// after running the transpiler
height = (user.height !== undefined && user.height !== null) ? user.height : undefined;
```

现在重构后的代码适用于旧的 JS 引擎和旧的浏览器。

![](img/33f507db37c38454313adce23b0b6ba4.png)

> 最著名的 transpilers 之一是 Babel。
> 
> 现代项目构建系统，例如 [webpack](https://webpack.js.org/) ，通过提供在每次代码变更时自动运行 transpiler 的方法，使得将它集成到开发过程中变得非常容易。

# 多填充物

新的语言特性可能不仅包括语法结构和操作符，还包括旧浏览器可能不支持的内置函数。

![](img/516e84e61f9bd331e9f2f04295d946e9.png)

例如，`Math.cbrt(n)`是一个返回一个数的立方根的函数，但可能老版本的浏览器不支持，在这种情况下这个方法会失败。

**Polyfill** 是更新/添加新功能的脚本。它填补了空白，并在需要时添加了缺失的实现。

对于这个特殊的例子，`Math.cbrt`的 polyfill 是一个实现它的脚本，如下所示:

```
if (!Math.cbrt) { // if no such function
  // implement it
  Math.cbrt = function(number) {
    // Math.pow exist even in ancient JavaScript engines
    return Math.pow(number,0.33);
  };
}
```

JavaScript 是一种高度动态的语言。随着每个新标准的出现，它可能会增加新的功能或修改旧的功能。

两个有趣的聚合填充库是:

*   [core-js](https://github.com/zloirock/core-js)
*   [polyfill.io](http://polyfill.io/)

您甚至可以调用 polyfill API 来获得一组已经缩小并准备好用于生产的 polyfill。下面是[环节](https://polyfill.io/v3/api/)。

# 结论

在向世界发布您的解决方案之前，请确保您记住这些概念，因为您不希望您的应用程序在一些旧的浏览器上失败。你甚至可以基于[的 webpack](https://webpack.js.org/) 和[的 babel-loader](https://github.com/babel/babel-loader) 插件建立一个代码构建系统，以便于使用，这样你以后就不需要手动进行 poly fills/trans filling 了。

![](img/91f410bdb736a34f032995b0a2bcd663.png)

如果你喜欢这篇文章，一定要看看我的其他文章，并关注最新的更新。

[](/what-is-webpack-ed18b68bd5d3) [## JavaScript 中的 Webpack 是什么？

### 我们大多数人在构建 JavaScript 应用程序时都听说过术语“Webpack”。这是什么？它是如何工作的…

javascript.plainenglish.io](/what-is-webpack-ed18b68bd5d3) [](/type-coercion-in-javascript-ef5e390d2318) [## JavaScript 中的类型强制

### 虽然 JavaScript 被认为是对初学者来说最简单的编程语言之一，但它也可能变得令人沮丧…

javascript.plainenglish.io](/type-coercion-in-javascript-ef5e390d2318) [](/event-loop-in-javascript-how-javascript-works-51c7bd73f07) [## JavaScript 中的事件循环:JavaScript 如何在幕后工作

### 事件循环是 JavaScript 异步编程背后的秘密。

javascript.plainenglish.io](/event-loop-in-javascript-how-javascript-works-51c7bd73f07) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***