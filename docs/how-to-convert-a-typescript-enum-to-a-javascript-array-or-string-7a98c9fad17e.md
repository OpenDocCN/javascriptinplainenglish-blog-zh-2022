# 如何将 TypeScript 枚举转换为 JavaScript 数组或字符串

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-typescript-enum-to-a-javascript-array-or-string-7a98c9fad17e?source=collection_archive---------12----------------------->

## 从 enum 中减去数据，并将其改造成 JavaScript 字符串数组，这样您就可以随心所欲地使用它了。

![](img/8eb3c9b3cf25a8b256ca971dbab79e1c.png)

Photo by [Joshua Woroniecki](https://unsplash.com/@joshua_j_woroniecki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

将 TypeScript 枚举转换成 JavaScript 数组非常容易，我经常用它来填充一个`<select>`,其中包含该枚举的所有值。

在这篇文章中，我喜欢向您展示如何从 enum 中减去数据，并将其改造成 JavaScript 字符串数组，这样您就可以随心所欲地使用它了。接下来，我们为它创建一个通用的实用函数，这样您就可以在整个应用程序中重用它。

## 什么是类型脚本枚举？

是的，我知道您正在寻找一个将 enum 转换成 JavaScript 数组的解决方案。但是你知道创建一个枚举有多种方法吗？

## 1.数字类型脚本枚举

数值枚举是 TypeScript 中最常用的。您可以像这样创建一个数字枚举。(*既然我爱🍕我们制作一个 PizzaToppings 枚举。*)

枚举中的第一个键的值为 0，第二个键的值为 1，依此类推。你不必为此做任何事。但是如果你想改变它，你可以。

通过这个，我们可以定义 enum 中每个键的值。

## 2.字符串类型脚本枚举

如前所述，字符串枚举是值为字符串的枚举。(*既然我爱🍕我们做一个枚举，我会选择 XL* 😅。)

通过这个枚举，我们可以从枚举中获取字符串值。如果您在应用程序中大量使用它们并且字符串值必须改变，那么这将非常方便😉。

所有这些枚举成员都是常量。但是如果您想让它们依赖于另一种数据类型，您可以让它们被计算。

我没有用过这个，但是根据 [TypeScript 文档](https://www.typescriptlang.org/docs/handbook/enums.html#computed-and-constant-members)这是可能的。

## 3.异构类型脚本枚举

你可能会问什么？我也是这么想的，哈哈！但这意味着一个枚举可以有混合的值、字符串和数字。(*你更喜欢哪种披萨？我还没尝过素食披萨😅)*

现在我们有了一个包含数值和字符串值的 PizzaTypes 枚举。

## 如何从 TypeScript 枚举中获取单个值？

有时，您需要应用程序中枚举的单个值。

让我们在订购比萨饼时创建顾客收据的一部分。

在真实的场景中，类型和风格不会被定义为 TypeScript 中的枚举，而是来自后端 API。但是对于这个例子，它工作得很好。

## 如何从 TypeScript 枚举中获取值？

现在我们知道了如何从 TypeScript 枚举中获取值，我们可以深入到我们的目标中，将多个值放入一个 JavaScript 数组中。

使用`Object.keys()`非常简单。

在示例中，您可以看到控制台将输出一个数组。有了枚举的键和值，我们可以用`.filter()`来防止这种情况。

现在我们可以看到，在控制台中，它将只显示值的字符串。

## 如何创建一个可重用的通用实用函数

既然我们知道我们的代码可以工作，我们可以创建一个超级方便的实用函数，它可以将我们所有的枚举(字符串和数字枚举)转换成 JavaScript 数组。

通过这个函数，我们可以看到这个函数既可以处理字符串也可以处理数字枚举。👍

# 谢谢！

![](img/34b6d4e88daa5f22c87d2b9b476f66e5.png)

读完这个故事后，我希望你学到了一些新的东西，或者受到启发去创造一些新的东西！🤗

如果我给你留下了问题或一些要说的话作为回应，向下滚动并给我键入一条消息。如果你想保密，请在 Twitter @DevByRayRay 上给我发一条 [DM。我的 DM 永远是开放的😁](https://twitter.com/@devbyrayray)

[**通过电子邮件获取我的文章点击这里**](https://byrayray.medium.com/subscribe) **|** [**购买 5 美元中等会员资格**](https://byrayray.medium.com/membership)

# 阅读更多

![RayRay](img/992af170033696163d6cc0269218aedd.png)

[雷雷](https://byrayray.medium.com/?source=post_page-----7a98c9fad17e--------------------------------)

## 最新的 JavaScript 和 TypeScript 故事

[View list](https://byrayray.medium.com/list/latest-javascript-typescript-stories-0358ad941491?source=post_page-----7a98c9fad17e--------------------------------)14 stories![](img/c93ca03b33796c40dcc47873de2697c2.png)![](img/86f37efa11855f6f0f0f62984c37f696.png)![](img/ddbaa6d0bea676316247e82043d60b63.png)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*