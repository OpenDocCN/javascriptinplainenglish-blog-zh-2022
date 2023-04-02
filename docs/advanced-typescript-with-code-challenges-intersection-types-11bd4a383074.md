# 具有代码挑战的高级类型脚本:交集类型

> 原文：<https://javascript.plainenglish.io/advanced-typescript-with-code-challenges-intersection-types-11bd4a383074?source=collection_archive---------6----------------------->

## 学习高级的 TypeScript 特性，并将它们应用到实际的代码练习中。

![](img/5b698621cee9ace700561513eecd9cb3.png)

Photo template by [Rachel Claire](https://www.pexels.com/de-de/@rachel-claire?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/de-de/foto/natur-feld-trocken-tier-4577793/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

TypeScript 太牛了！越来越多的项目将它作为主要的编程语言。尤其是在前端开发领域，构建大型应用程序变得至关重要。虽然像 Angular 这样的框架提供 TypeScript 作为主要语言，但所有已知的库，如 React 或 Vue.js，都支持静态类型语言。

> 它不仅是最流行的语言之一，也是发展最快的语言之一。— [GitHub](https://www.businessinsider.com/most-popular-programming-languages-github-2019-11#7-typescript-4)

作为发展最快的编程语言之一，越来越多的功能被不断添加。每增加一项新功能，它都会变得更加强大。掌握它们会让你的代码更健壮、更整洁、更容易重构。在本文中，我们将了解更多关于交集类型的知识，这是 TypeScript 中较为复杂的概念之一。之后，我们将在一次实际的代码挑战中应用我们所学的知识。

> […]它非常类似于 JavaScript，但是具有更强大的功能，可以帮助开发人员构建大规模的应用程序。”— [GitHub](https://www.businessinsider.com/most-popular-programming-languages-github-2019-11#7-typescript-4)

要了解关于高级 TypeScript 特性的更多信息，请查看我的其他文章。以下是一个概述:

Overview Typescript Features

[](https://web-highlights.com/) [## 网络亮点- PDF 和网络荧光笔

### Web Highlights 是一个在 Web 上突出显示文本的工具，可以更有效地组织您的研究。提升你的…

web-highlights.com](https://web-highlights.com/) 

# 交叉点类型

交集类型是最常用的 TypeScript 特性之一，与[联合类型](https://medium.com/@mariusbongarts/advanced-typescript-with-code-challenges-union-types-2474c6e62097)密切相关，但它们的用法不同。虽然我们可以使用联合类型来组合和分离现有的类型，但是**交集类型**允许我们将类型加在一起以获得一个具有所有类型的所有特性的新类型。

虽然我们对联合类型使用`|`操作符来分离类型，但是我们可以对交集类型使用`&`操作符来组合类型。

例如，当我们像这样组合三种类型时:

Intersection types

`AllRoles`类型将拥有`User`、`Admin`和`Guest`的所有属性。请注意，在组合类型时，顺序并不重要。

这意味着如果我们的界面看起来像这样:

当使用`AllRoles`类型分配一个新变量时，我们需要添加所有属性:

## 与联合类型的比较

有时我发现对比对立的类型脚本功能很有帮助。所以，让我们重温一下 [**工会类型**](https://medium.com/@mariusbongarts/advanced-typescript-with-code-challenges-union-types-2474c6e62097) 。假设我们使用一个[联合类型](https://medium.com/@mariusbongarts/advanced-typescript-with-code-challenges-union-types-2474c6e62097)而不是交集类型作为我们的接口，如下所示:

然后，只需要向我们分配的`AllRoles`变量添加一个属性就足够了:

# 代码挑战💻

你可以在这个[打字稿操场(起始码)](https://www.typescriptlang.org/play?ts=4.7.4#code/PQKhCgAJoeQVwE6QMYHsAmBTARgQwM6YqoB2ALrgJYn6S6QAKmC+pAIgCoySrYBWmZGUgB3SmQAWkVgFsiuMmQSVscMpnwA6KNB2QAcqhEAaUURG5ykMqkiYAHktxDrEoiUwjrATwAORAGFSCiE2BXoAMwRUGR5EHn5BYUkFSD00cioaYkyXagjUBBkFSlI6bFQ1Okh-FlJNNOhG6AAxRElmGULMU1wAGz6ff1pUCNdUjy8yPyJ8CUq+9EhsWaVqAHNtPQBRe2RmZEpCAC49ZugARgaAhEwFd08hwODnMjCKM4AmBoBZXABrZ65N7hJ48Eh9bw5CjUVwaIiSW5EQHefDHOzFSh9AAFpl88w8uMgXWwWMwZwAzL8AfIBk9aDZlkRRmD8GsSOszgAWBotSj2Oh0jgzfDIZS+YTMaIscBQEDAWXgajqBARZxEJh1EhsRkAbx0EUoLDI+lwcnRbOUHIA3Do+gQTWbMBb2etbdBMJi+i6rW6dPjSM7ICQ4DIVgh3cTeGT0SGw8xbQBfWVpab+SBBYHvegAXkYzFY2pstvAGTZkEN9g4EiOwv82wQ0vRus9VG90ldeIJQctG1MJJjHd9icged1I4IkDgJH+JCMJDotEzIRBFGtaXAQA)里解习题。如果你被卡住了，你可以在这个[类型脚本游乐场(解决方案代码)](https://www.typescriptlang.org/play?ts=4.7.4#code/PQKhCgAJoeQVwE6QMYHsAmBTARgQwM6YqoB2ALrgJYn6S6QAKmC+pAIgCoySrYBWmZGUgB3SmQAWkVgFsiuMmQSVscMpnwA6KNB2QAcqhEAaUURG5ykMqkiYAHktxDrEoiUwjrATwAORAGFSCiE2BXoAMwRUGR5EHn5BYUkFSD00cioaYkyXagjUBBkFSlI6bFQ1Okh-FlJNNOhG6AAxRElmGULMU1wAGz6ff1pUCNdUjy8yPyJ8CUq+9EhsWaVqAHNtPQBRe2RmZEpCAC49ZugARgaAhEwFd08hwODnMjCKM4AmBoBZXABrZ65N7hJ48Eh9bw5CjUVwaIiSW5EQHefDHOzFSh9AAFpl88w8uMgXWwWMwZwAzL8AfIBk9aDZlkRRmD8GsSOszgAWBotSj2Oh0jgzfDIZS+YTMaIscBQEDAWXgajqBARZxEJh1EhsRkAbx0EUoLDI+lwcnRbOUHIA3Do+gQTWbMBb2etbdBMJi+i6rW6dPjSM7ICQ4DIVgh3cTeGT0SGw8xbQBfWVpab+SBBYHvegAXkg+ugAG0GNFatNILCUSyGJRkP8ADya1jamymADkAY8bcgAB9IG2SWTu32256qH02wA+AC6Po2SdlGTZkEN9g4EiOwv82wQ0vRurHWLnHLxBKDlo2pkHfXPrsTkDzuvvBEgcBI-xIRhIdFomZCIIoa00nAIA)中找到解决方案。当然，你也可以复制&粘贴类型脚本代码到你选择的 IDE 中。

## 介绍

我们的代码库包含两个接口:`UserInfo`和`ContactInfo`。

现在，我们想要创建新的类型`User`，它包含来自`UserInfo`和`ContactInfo`的所有属性。

1.  创建新类型`User`
2.  使用`&`运算符将类型`UserInfo`和`ContactInfo`相交
3.  修复所有类型脚本错误

## 密码

下面是本次练习的 [**起始码**](https://www.typescriptlang.org/play?ts=4.4.4#code/PQKhCgAJoeQVwE6QMYHsAmBTARgQwM6YqoB2ALrgJYn6RkDuqk1ZmCAZrspvgFyQBVQggCSJdk1wl0kAMKkKyMmIlRoayADlU9ADSR6RelLJ0myBJlys6ACyIlM9OgE8ADkSFs715iWQANnBYtLgBAZBuCKgeCGSUPJDs0QC2gsIqktJyClzK4qgAdOAaAKIAHtwIyJSEvBqQDQCMhXKW1g5Orh7pbA0ATK1edkQAZJAxbNaoSBJILGyEStQA5iPdiV6iBZBSMvLkeZkNAMytAGKU5bvhkAAq7jwWlG6mbNEI+CWQIMAlCxwuJ4MjsAN4NEi4FKYfj4MgIVYAbnAAF9-uQ2JxuDlDkpMpBwdBoJgUlQArD4UiGm5bKQYZASHAUtg2Mi0eAyI9ekgALwElHIkrAYCQS7XMj2DaQd4zAyUCXUOy1JJwfzxUjgdiq5akOg8MgACjgwn4WwAlASGmgaKgAphCgFUCsjcJCpDofpjWxCiSyZ7XTS6Wa2eAgA) :

## 解决办法

下面是本练习的 [**解法代码**](https://www.typescriptlang.org/play?ts=4.4.4#code/PQKhCgAJoeQVwE6QMYHsAmBTARgQwM6YqoB2ALrgJYn6RkDuqk1ZmCAZrspvgFyQBVQggCSJdk1wl0kAMKkKyMmIlRoayADlU9ADSR6RelLJ0myBJlys6ACyIlM9OgE8ADkSFs715iWQANnBYtLgBAZBuCKgeCGSUPJDs0QC2gsIqktJyClzK4qgAdOAaAKIAHtwIyJSEvBqQDQCMhXKW1g5Orh7pbA0ATK1edkQAZJAxbNaoSBJILGyEStQA5iPdiV6iBZBSMvLkeZkNAMytAGKU5bvhkAAq7jwWlG6mbNEI+CWQIMAlCxwuJ4MjsAN4NEi4FKYfj4MgIVYAbnAAF9-uQ2JxuDlDkpMpBwdBoJgUlQArD4UiGm5bKQYZASHAUtg2Mi0eAyI9ekgALzc-HjA6KfISZElYDASCXa5kewbSDvGYGSiy6h2WpJOD+eKkcDsLXLUh0HhkAAUcGE-C2AEoCQ00DRUAFMIUAqgVubhIVIdD9Ba2IUSWS-V6aXTrWzwEA) :

# 最后的想法

我希望你喜欢阅读这篇文章。我将在后续文章中发布更多关于高级 TypeScript 特性的文章。我还写关于 Web 组件、前端框架、软件设计原则和许多其他主题的文章。

我总是乐于回答问题，并乐于接受批评。请随时联系我😊通过 [LinkedIn](https://www.linkedin.com/in/marius-bongarts-6b3638171/) 联系我，在 [Twitter](https://twitter.com/MariusBongarts) 关注我，或者[订阅](https://medium.com/subscribe/@mariusbongarts)通过电子邮件获取我的故事。

[**这里是无限制访问媒体上每一个内容的链接**](https://medium.com/@mariusbongarts/membership) **。如果你用这个链接注册，我会赚一小笔钱，不需要你额外付费。**

[](https://medium.com/@mariusbongarts/membership) [## 通过我的推荐链接加入 Medium-Marius bong arts

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@mariusbongarts/membership) 

# 关于作者

我是埃森哲软件工程分析师宋。最驱动我的是我想创造一些可能对他人有帮助并改变他人生活的东西的冲动。

比如你是否厌倦了浏览自己的历史来寻找前几天看到的信息？我的 [**网站重点介绍 Chrome 扩展**](https://chrome.google.com/webstore/detail/web-highlights-%20-bookmark/hldjnlbobkdkghfidgoecgmklcemanhm) 覆盖了你，并将通过以结构化和高效的方式组织你的研究来提高你的生产力。就像你在书和文章上做的那样，突出显示任何网页或 PDF 上的文本。你的精彩片段会直接同步到 web-highlights.com[的网络应用上，你可以在任何地方找到它们。](https://web-highlights.com/)

[](https://chrome.google.com/webstore/detail/web-highlights-pdf-web-hi/hldjnlbobkdkghfidgoecgmklcemanhm) [## Web 亮点— PDF 和 Web 荧光笔

### 在每个网站或 PDF 上创建亮点、书签、标签和文件夹。以结构化的方式组织您的想法和研究…

chrome.google.com](https://chrome.google.com/webstore/detail/web-highlights-pdf-web-hi/hldjnlbobkdkghfidgoecgmklcemanhm) 

## 进一步阅读

[](https://medium.com/@mariusbongarts/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [## 我的第一个 9.99 美元之旅与我的副业

### Chrome 扩展带来的被动收入

medium.com](https://medium.com/@mariusbongarts/my-journey-to-the-first-9-99-with-my-side-project-3edc13dd1f2d) [](/will-web-components-replace-frontend-frameworks-535891d779ba) [## Web 组件会取代前端框架吗？

### 它们是为解决不同的问题而构建的。

javascript.plainenglish.io](/will-web-components-replace-frontend-frameworks-535891d779ba) [](/showcase-your-medium-articles-with-web-components-part-1-basics-d2c6618e9482) [## 用 Web 组件构建自己的博客组合:基础

### 第 1 部分—定制元素、阴影 DOM 和 HTML 模板

javascript.plainenglish.io](/showcase-your-medium-articles-with-web-components-part-1-basics-d2c6618e9482) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**