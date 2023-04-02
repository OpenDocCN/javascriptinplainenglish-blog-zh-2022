# 如何获得两个 JavaScript 对象之间的差异

> 原文：<https://javascript.plainenglish.io/how-to-get-the-difference-between-two-javascript-objects-e885e09382cb?source=collection_archive---------8----------------------->

## 使用洛达什`isEqual`方法获取两个对象之间不同的键列表。

在调试 JavaScript 应用程序时，了解对象之间的差异通常很有用，例如，当 React 组件重新呈现时，查看提供给它的`props`中发生了什么变化。

![](img/17f6d6b1f32bf275eb8bba5e9b5f40fa.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

该功能使用[洛达什](https://lodash.com/) `isEqual`方法，快速为您提供两个对象之间不同的键列表:

用两个对象调用此函数将返回值不相等的对象上的键的名称数组，还包括两个对象上不存在的键的名称。一旦您掌握了这些顶级信息，您就可以根据需要进行更深入的挖掘，以了解它们之间的确切差异。

该函数还提供了一个比较对象属性引用的选项，在这种情况下，如果两个对象的键值相同，但是引用不同，则返回键名，并在末尾添加`(ref)`。例如，在使用浅层比较来决定是否重新渲染纯组件的情况下，这一点尤其相关。

*更内容于*[***plain English . io***](https://plainenglish.io/)*。**[***免费周报***](http://newsletter.plainenglish.io/) *。跟随我们登上* [***推特***](https://twitter.com/inPlainEngHQ) 和*[***领英***](https://www.linkedin.com/company/inplainenglish/) *。加入我们的**[***社群不和***](https://discord.gg/GtDtUAvyhW) *。****