# 我回顾了两年前我的第一个项目。以下是我学到的 4 个教训。

> 原文：<https://javascript.plainenglish.io/i-reviewed-my-first-project-built-2-years-ago-here-are-4-lessons-i-learned-568130046d04?source=collection_archive---------16----------------------->

## 我被我的第一个项目吓坏了！

![](img/926ffd80582ccfc230820c94463aa66a.png)

Photo by [Sebastian Herrmann](https://unsplash.com/@officestock?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都是从某个地方开始的，如果你不畏惧过去的自己，这通常意味着你没有成长为一个人。

最近，我在回顾和更新我的旧项目，这样我就可以把它们添加到我的投资组合中，但令我惊讶的是，即使是早在去年 7 月的项目，与我目前的标准相比，也显得如此平庸。

这些项目工作得非常出色——没有任何问题，但困扰我的是代码。

我坐下来重构代码，注意到底层堆栈和架构无懈可击，处理问题的逻辑也是如此。

这时我意识到真正的问题是结构和代码，以及对可用技术的轻微无知。

我使用 Flutter 构建了一个新闻应用程序，该应用程序需要调用一个 API 来获取最新的新闻文章。我使用 Node.js 构建了 API，这是我的第一个 web 应用项目。

这是一个简单的 API，它基本上调用了另一个 API &缓存了一个小时的响应，然而，我犯了太多的错误，甚至这样一个简单的 API 对我的眼睛来说也变得不可读和太复杂了。

这是一个不同于我通常的博客类型，所以任何反馈都是非常感谢的。

以下是我从这个项目中学到的 4 点经验:

## 1.没有文件结构

![](img/83e7f1d0d668f0d63e25d814d18e1550.png)

[Source](https://blog.logrocket.com/organizing-express-js-project-structure-better-productivity/).

当您在几个月(或几年)后重访项目时，一个适当的文件夹结构可以简化对代码的审查。

理想情况下，Express 应用程序应该看起来像上面分享的图片，但我的 Node.js 应用程序没有任何文件夹。

一个 Node-API 应用程序通常会有一些路由和控制器。

所有文件都在根文件夹中，并且命名不正确。文件名只会让事情更加混乱。

文件夹结构对生产力和可维护性很重要，公平地说，我一直认为这是理所当然的，直到去年晚些时候，当我构建我的第一个 SaaS 时，才意识到正确的结构是如何帮助我扩展它的。

## 2.无知的态度。

[Source](https://giphy.com/gifs/SmithsonianNMNH-smithsonian-hans-sues-such-ignorance-is-best-ignored-if58SMTqYmTDbK2XyH).

在大学里，我们被教授排序数组的实际逻辑和实现，比如冒泡排序。

我没有意识到 JavaScript(和大多数语言)有一个内置的排序函数已经足够了，特别是对于一个只有 100-150 个条目的新闻文章列表。甚至一个简单的谷歌搜索“如何排序一个数组？”会显示排序函数的用法。

然而，我却浪费了几个小时来编写和完善排序算法。

此外，由于我必须缓存响应，我可以使用更简单的方法，比如使用记忆化或使用全局变量。

然而，我决定从 Stack Overflow 复制代码来创建一个文件，并在那里编写我的 JSON 对象数组。

虽然这是一种有效的方法，但我对创建和更新文件一无所知，纯粹是复制代码，甚至连一半都不懂。

更糟糕的是，我不得不稍微修改了一下，由于我当时缺乏理解，代码变得杂乱无章。

这是一个奇迹，它的工作！

> “给我六个小时去砍树，我会用前四个小时磨斧子”—亚伯拉罕·林肯

在开始编码之前进行研究是很重要的。我仍然记得我花了无数时间编写后端代码，而如果我知道有更好的解决方案和实践，我可以在一两天内完成。

## 3.不必要的&错误的包装。

如果我没记错的话，我知道 Heroku(我用来部署服务器的平台)允许的最大 slug 大小是 500MB。

只要我在这个限制之下，我就不会考虑优化我的包大小。

当我从一个不同的 API 获取数据到我的 Node.js 服务器上时，fetch 没有内置在 Node.js 中，我使用了多个库，比如 Axios、Node-fetch 和 [Needle](https://www.npmjs.com/package/needle) 。

我也安装了多个解析器，用于处理我得到的 API 数据。

最后，我最终使用了 Axios 和一个解析器，没有移除所有未使用的包。

当然，随着时间的推移，我逐渐明白了包大小的重要性。更大的包意味着用户必须传输更多的数据，同时也增加了构建时间。特别是，当我使用 GitHub Actions 构建自己的 CI/CD 管道时，包的大小和构建时间变得更加重要。

这是疯狂的想法，2 年后，我变得非常快，删除任何我不使用的包。我现在痴迷于删除不必要的代码和包。

## 4.没有代码分裂的迹象。

我写了可怕的代码。我所说的可怕，是指极其丑陋和多余的代码。

我有多个全局声明的未使用的变量，而且我没有完全掌握这门语言，所以输入了大量的手动实现。

在整个项目中，我一次又一次地违反了干燥原则。

所以基本上，获取 API 的函数超过 45 行，现在我可以用不到 10 行代码来完成。但是当时我不知道头和 JSON 主体的要求，所以我基本上是复制粘贴，直到它正常工作。

但是获取数据并解析它的整个文件有 383 行长！

代码分割实际上是一门艺术，我相信随着时间的推移，我在这个部门已经有了很大的进步。

对于外行来说，代码分割基本上是一种将大文件分割成多个小文件的方法，这些小文件可以按需请求。

这也使得调试文件更加容易。

下面是代码拆分的一个示例:

```
// app.js
import { add } from './math.js';

console.log(add(16, 26)); // 42// math.js
export function add(a, b) {
  return a + b;
}
```

与将它们写入单个文件相比:

```
function add(a, b) {
  return a + b;
}

console.log(add(16, 26)); // 42
```

当然，这是一个简单的单行函数，但是在实际的应用程序中，您可以想象一个函数，它接受一个 URL 和一个字符串(HTTP 方法，如“POST”)作为参数，并使用它来获取 URL 并返回它。

代码分割使我现在创建项目变得非常容易，因为它方便了项目的维护，对我来说另一个好处是我可以在不同的项目中重用代码。

## 最后的想法…

回顾别人的项目是一个很好的学习方式，但是看到你过去的项目，注意到你可以做得更好的事情，反映出你已经成长为一个更好的程序员。

重访我的第一个项目让我想起了我卑微的出身，我相信每个自学成才的开发人员都会有这种感觉。

这是一个不同类型的博客，我希望你喜欢它。

**如果你喜欢阅读这篇文章，可以考虑使用** [**我的推荐链接**](https://medium.com/@anuragkanoria/membership) **，这样你就可以通过点击** [**这里**](https://medium.com/@anuragkanoria/membership) **无限制地访问我的博客以及其他作者的博客。**

另外，请查看我最新的关于 web 开发框架生态系统使用和流行选择的总体展望的博客。

[](/why-dont-we-use-other-frameworks-instead-of-react-3fcfaec5604b) [## 为什么不用其他框架代替 React 呢？

### React 到底为什么这么受欢迎？

javascript.plainenglish.io](/why-dont-we-use-other-frameworks-instead-of-react-3fcfaec5604b) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*