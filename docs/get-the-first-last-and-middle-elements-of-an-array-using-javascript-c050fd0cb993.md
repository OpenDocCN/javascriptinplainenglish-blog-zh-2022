# 使用 JavaScript 获取数组的第一个、最后一个和中间的元素

> 原文：<https://javascript.plainenglish.io/get-the-first-last-and-middle-elements-of-an-array-using-javascript-c050fd0cb993?source=collection_archive---------7----------------------->

使用 ES6 获取数组的第一个、最后一个和中间的元素。

![](img/064b43872adaaee4a8cc69f50252c546.png)

Photo by [Daniel K Cheung](https://unsplash.com/@danielkcheung?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近我想把一个数组拆开，这样我就可以用 ES6 得到数组的第一个、最后一个和中间的元素。我在一个旧网站[ComeExploreCanada.com](https://www.comeexplorecanada.com/ontario/dryden)工作，我需要在网站上添加面包屑。第一个链接有一个图标，中间的链接样式相同，最后一个链接没有样式。我的想法是，如果我有一个链接数组，我可以对第一个和最后一个链接以及所有不是第一个或最后一个(中间)链接的元素做一些不同的事情，我可以将它们设计成相同的样式。

![](img/9e8bf103c1ee427485e72a930681e092.png)

Website Breadcrumbs

# 如何在 JavaScript 中找到一个数组的第一个、最后一个和中间的元素？

为了获得数组的第一个、最后一个和中间元素，我们可以使用 [ES6 析构赋值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)将数组中的值解包到不同的变量中。

看看下面的例子。这就是在 JavaScript 中获取数组的第一个、最后一个和中间元素的方法。

让我们来谈谈上面例子中的第 3 行发生了什么。我们获取数组`arrayData`并从中析构(创建)一个对象。因为我们正在析构一个数组，所以我们得到数组索引作为对象键。

*   `0: first` —我们将零数组索引重命名为属性名`first`
*   `[arrayData.length — 1]: last` —我们将最后一个数组索引重命名为属性名`last`。因为数组长度是动态的；这意味着不同的数组会有不同的长度，这就是我们做`arrayData.length — 1`的原因。上例中基本是`4: last`。
*   `...rest` —我们可以使用 [Spread 语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)来获取剩余的数组元素，这将为我们提供数组的“中间”项。

希望下面的例子能让你更好地了解正在发生的事情。

如果您不熟悉 ES6 JavaScript，让我们采用一种更简单的方法来获取字符集合的第一个和最后一个元素。

零总是数组中的第一项。为了得到数组中的最后一项，我们可以取数组的长度，然后减去`1`。在上面的例子中，`arrayData`的长度是`5`，但是数组是[从零开始的](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections)，这意味着第一项是`0`而不是`1`，所以我们必须从数组长度中减去`1`，得到数组中的最后一个索引`4`。

# 创建一个 Util 函数来返回数组中的第一个、最后一个和中间的元素

下面我提供了两个不同的函数，用 ES6 返回数组中的第一、最后和中间的项。下面的第一个版本返回一个数组，而第二个版本返回一个对象。去查查他们俩。对于每一个，我都使用 Jest 提供了 JavaScript、TypeScript 和测试。

```
// Returns array version
const [first, middle, last] = buildFirstMiddleLastList(arrayData);
```

这个辅助示例返回一个对象，您可以使用析构来获取第一个、最后一个和中间值。

```
// Returns object version
const {first, middle, last} = buildFirstMiddleLastList(arrayData);
```

如果你喜欢这篇文章，请分享它，关注我，阅读我的其他[文章](https://medium.com/@robertsavian)和/或用我下面的推荐链接注册 Medium。谢谢！

[](https://medium.com/@robertsavian/membership) [## 通过我的推荐链接加入 Medium-Robert S(代码带)

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@robertsavian/membership) 

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***