# 在 JavaScript 中将 2d 数组映射到 1d 数组

> 原文：<https://javascript.plainenglish.io/js-map-2d-array-to-1d-array-33dafbec9aec?source=collection_archive---------11----------------------->

## 用单行代码将 2d 数组转换为 1d 数组

![](img/227df10491b6fc63bfc97be75fffa5be.png)

Photo by [Dose Media](https://unsplash.com/@dose?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇短文将用一行代码解释如何将 2D 数组转换成 1D 数组。基本上，你需要为 2D 数组使用 [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 和 [spread 运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)。

用 2D 数列检查下面的例子:

```
const numbers = [[1,2], [2,3], [3,4]];
const result = [].concat(...numbers)

// result: [ 1, 2, 2, 3, 3, 4 ] 
```

感谢阅读。

*如果你喜欢这样的故事，并且想继续阅读我的故事，请考虑成为* [*中等会员*](https://medium.com/membership) *。每月 5 美元，你可以无限制地访问媒体内容。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)***

***用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。*