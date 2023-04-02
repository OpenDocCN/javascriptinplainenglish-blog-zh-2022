# 什么是 TypeScript 中的模块？

> 原文：<https://javascript.plainenglish.io/what-is-a-module-in-typescript-574012b848fa?source=collection_archive---------17----------------------->

## 用简单的话理解打字稿中的模块

![](img/67071041c8dcbe6e323dc0496ea35727.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 TypeScript 中，我们可以将模块作为一种在局部范围内执行组的方式，而不是在全局范围内执行。换句话说，这可以总结为——在模块内部声明的所有内容都不能在模块外部访问。

这是在局部范围内执行某项任务的一种非常有效且最优的方式。除了 TypeScript 之外，我们还将 JavaScript 中的模块称为一种重用代码的方法，通过分解代码来制作单独的文件。

模块被广泛用于通过创建局部范围文件来避免代码的全局范围。我们可以进一步将模块分为两类—

## 内部模块

这是一种模块，基本上包含在旧类型的 TypeScript 中，后来进行了更新。这可用于将 TypScript 函数分组到一个文件中。

用更简单的话来说，我们可以称内部模块为一种将不同的类、函数和接口创建成一个文件的逻辑分组的方法。

正如我已经提到的，这种类型的模块出现在旧版本的 TypeScript 中，因此在当今时代没有支持或用例。它被命名空间所取代。

让我们看一个新旧模块的例子——

```
Internal Module (OLD VERSION) -->module example{
export function add(x,y){
console.log("result:"(x+y));
}
} Namespace (NEW VERSION) -->namespace example{
export function add(x,y){
console.log("result:"(x+y));
}
}
```

## 外部模块

这是 TypeScript 中模块的第二个类别。正如我们之前在内部模块中所讨论的，在新版本中它被命名空间所取代，而内部模块现在不再使用。换句话说，现在外部模块被称为模块。

众所周知，在编写完整的代码时，我们需要处理各种文件。有时这些文件可能包含大量代码，如果没有模块方式，处理所有这些文件似乎是不可能的。

在技术术语中，它用于确定不同 js 文件之间的负载依赖关系，因此人们可以简单地猜测，如果我们使用单个文件而不是多个文件，它是没有用的。

模块无疑是类型脚本的一个非常有趣和重要的分支。当我们讨论内部和外部模块时，我们可以简单地指出这样一个事实:内部模块目前没有使用，名称空间用于创建组。也可以参考 TypeScript 中关于模块的 [*文档*](https://www.typescriptlang.org/docs/handbook/modules.html) 来深入探讨这个话题。

这是它希望这是信息，它给你一个什么样的模块在 TypeScript 概述。祝你的编程之旅好运！

[***用我的推荐链接给自己买一个 5 美元的中级会员，点击这里(我得到一小笔佣金，它直接支持我，不需要你额外付费)***](https://aniketz.medium.com/membership)

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 阅读 Aniket 上的每一个故事(以及媒体上成千上万的其他作者)。你的会员费直接支持了一个市场…

aniketz.medium.com](https://aniketz.medium.com/membership) 

[***想加入我的时事通讯获取更多这样的内容，点击这里…***](https://aniketz.medium.com/subscribe)

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*