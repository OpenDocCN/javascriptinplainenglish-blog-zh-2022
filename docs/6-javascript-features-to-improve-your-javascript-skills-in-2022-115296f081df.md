# 2022 年提高你的 JavaScript 技能的 6 个 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/6-javascript-features-to-improve-your-javascript-skills-in-2022-115296f081df?source=collection_archive---------4----------------------->

## 这些特性都是非常新的特性，并且改进了 JavaScript 中已经存在的功能。

![](img/0a3ace880a3bcca5691da62673d0479f.png)

最近，所有主流浏览器都更新了 JavaScript 特性。因此，在这篇文章中，我将深入研究这六个值得一提的功能，以提高你在 2022 年的 JavaScript 技能。

这些特性都是非常新的特性，并且改进了 JavaScript 中已经存在的功能。

# 1.用`Array.at()`获取 JavaScript 数组项

## 以前

先说`Array.at()`法。从 JavaScript 早期开始，我们就一直使用这种语法从数组中获取具有已知索引的特定元素。

## 在...之后

目前来看，这工作得非常好。但是《T2》更具可读性。因此，使用这种方法，我们可以以一种可读性更好的方式从上面编写代码。

语法变得更短，尤其是最后一个或第 n 个元素。

如果数组索引不存在，您仍然会得到一个`undefined`值，所以那里没有任何变化。

*When the code doesn’t run, select the newest Node version 👆 or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-array-at-method)

## 浏览器支持

在我看来，浏览器支持是完美的。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。在 de MDN 网络文档中找到更多[信息和示例。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at)

# 2.使用 structuredClone()深度复制 JavaScript 对象

如果你想创建一个 JavaScript 对象的副本，大部分时间它会变成一个浅层副本。

## 传播运算符副本

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-shallow-copy-spread-operator)

这意味着更新嵌套属性(不是顶级属性)也会影响浅表副本。

## JSON 解析和字符串

制作深层副本需要更多的东西。为此我们需要`JSON.parse(JSON.stringify(object))`。这感觉像是一个黑客，但它完成了工作。

*When the code doesn’t run, select the newest Node version 👆 or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-deep-copy-json-parse-stringify)

当您运行这段代码时，您将看到原始的`myBrowser`正在被更新，但是深层副本`myBrowserCopy`没有被更新。所以用`JSON.parse(JSON.stringify(object))`你可以创建深层拷贝。

## 结构化克隆()

您可以使用更简单的方法来创建对象的深层副本。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-deep-copy-structuredclone/2.0.0)

正如您所看到的，这个方法有更好的可读性，因为它表示您克隆了那个对象。

## 浏览器支持

在我看来，对浏览器的支持很棒。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。此外，请记住，有些浏览器不支持这种工作方式。在 de MDN 网络文档中找到更多[信息和示例。](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)

# 3.顶级等待

从 ES2017 开始，我们为同步写承诺提供了 async/await。

## 以前

唯一的条件是在 JavaScript 中使用`await`。您需要让您的函数`async`，这有时有点麻烦。因为你不想在每个用到`await`的函数前都写`async`，对吧？

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-async-await)

*写一个* [*我* FFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) *每次想用* `*await*` *也挺难看的🤭。* *当代码不运行时，选择最新的节点版本👆*

## 在...之后

嗯，现在我们可以不用`async`而用`await`💪

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/top-level-async-await)

现在你不再需要任何 IFFE 样板文件了🔥。我们需要写`await`；好了😀！记住类中的方法仍然需要在它前面有`async`关键字；不然就不行了。

## 浏览器支持

在我看来，[浏览器支持很棒](https://caniuse.com/mdn-javascript_operators_await_top_level)。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。在 de V8 文档中找到更多[信息和示例。](https://v8.dev/features/top-level-await)

# 4.等待

我不知道这个用例是否发生在你身上，但对我来说，它发生了。

假设您需要一个接一个地进行多个 AJAX 调用，但是您希望对它们进行循环。但是在循环过程中，这些承诺还没有解决。那你怎么办？

## 以前

不久前，只能等到所有这些承诺都兑现之后。在解析之后，你可以对它们进行循环。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-loop-over-multiple-promises)

在运行这段代码时，您可以看到，如果其中一个承诺没有被解决而是被拒绝，for 循环甚至不会开始遍历它们。

## 在...之后

但是由于有了`for await...of`，您可以将 for 循环与`Promise.all()`功能结合起来。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/for-of-await)

如你所见，这在我看来更好读。而且每解决一个承诺，循环到下一个承诺，太棒了！

但是当一个承诺被拒绝时，for 循环就会停止。如果你想在一个承诺被拒绝时循环继续，你需要使用`Promise.allSettled()`。用这个方法，你可以看到哪些承诺被拒绝了，哪些兑现了。(查看 [MDN 网络文档了解更多关于 Promise.allSettled](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled) 的信息。)

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-loop-over-promises-with-allsettled)

## 浏览器支持

在我看来，[浏览器支持很棒](https://caniuse.com/mdn-javascript_statements_for_await_of)。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。在 de MDN 网络文档中找到更多[信息和示例。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)

# 5.私有类字段

每个花一些时间在 TypeScript 上的开发人员都知道`private`关键字。这表明属性或方法只在该类中使用。但是在浏览器中，你可以看到那些字段和方法是公开的，就像公共的一样。

从现在开始，我们可以通过在方法的属性前面加上#来使它成为私有的。这不仅仅是语法上的好处，而且它不会将那个字段或方法暴露给外部。

*Sorry no Runkit embed, the private class fields are not supported by them ☹️*

如果您在控制台中记录整个类，您可以看到私有字段存在，但是当您试图调用它时，您会收到一个语法错误。私有字段可以用公共方法在类外公开。

# 浏览器支持

在我看来，[浏览器支持很棒](https://caniuse.com/mdn-javascript_classes_private_class_fields)。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。在 de MDN 网络文档中找到更多[信息和示例。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)

# 6.Object.hasOwn

有时我们喜欢在试图访问一个对象之前检查它是否有特定的属性。是的，我知道有类似[可选链接](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)的东西😉。

*如果你要很多次检查这些东西，请考虑打字稿。跟着我的* [*打字新手指南*](https://levelup.gitconnected.com/typescript-for-beginners-97b568d3e110) *。*

多年来，我们在 JavaScript 中使用了`Object.prototype.hasOwnProperty()`方法。当您使用此方法时，它会返回一个布尔值。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-object-prototype-hasownproperty)

但是当我们试图做出一个这样的物体时，它就会变得令人困惑。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-object-create-hasownproperty)

因为通常，当你创建一个对象(`const obj = {}`)时，该对象从`Object.prototype`获得所有默认属性和方法，但是当你将`null`作为一个值给 create 方法时，它不会从`Object.prototype`获得任何东西，所以这就是为什么`hasOwnProperty`方法不在该对象上。

有了`Object.hasOwn`，你就没有那个问题了。

*When the code doesn’t run, select the newest Node version 👆or try it on* [*Runkit*](https://runkit.com/devbyrayray/javascript-object-create-with-object-hasown)

## 浏览器支持

***注:*** `*Object.hasOwn()*` *意在替代* `[*Object.hasOwnProperty*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)` *。*

在我看来，[浏览器支持很棒](https://caniuse.com/mdn-javascript_builtins_object_hasown)。希望您不需要支持旧的 Internet Explorer 浏览器，因为它们缺乏支持。在 de MDN 网络文档中找到更多[信息和示例。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn)

# 谢谢！

![](img/2addcdd3a08d3c1e2fed7569933fc6cf.png)

读完这个故事后，我希望你学到了一些新的东西，或者受到启发去创造一些新的东西！🤗

如果我给你留下了问题或一些要说的话作为回应，向下滚动并给我键入一条消息。如果你想保密，请在 Twitter @DevByRayRay 上给我发一条 [DM。我的 DM 永远是开放的😁](https://twitter.com/@devbyrayray)

[**通过电子邮件获取我的文章点击这里**](https://byrayray.medium.com/subscribe) **|** [**购买 5 美元的中等会员资格**](https://byrayray.medium.com/membership)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*