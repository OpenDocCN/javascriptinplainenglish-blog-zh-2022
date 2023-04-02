# 为什么现在使用 TypeScript 进行 JavaScript 开发

> 原文：<https://javascript.plainenglish.io/why-use-typescript-for-javascript-development-today-c6561b70a34b?source=collection_archive---------8----------------------->

![](img/2d7fe17bc5f6f96d5394f472cc6d261b.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TypeScript 是一种由微软开发和维护的开源编程语言。它是 JavaScript 的类型化超集，这意味着所有 JavaScript 代码都是有效的类型脚本代码。尽管如此，TypeScript 还是增加了一些额外的特性，使得编写和维护大型复杂的代码库变得更加容易。

TypeScript 之所以重要的一个主要原因是，它允许开发人员向他们的代码添加类型批注。这意味着他们可以指定变量、函数参数和返回值的数据类型，这有助于防止许多常见的错误，并使代码更容易阅读和理解。

# 没有类型的函数

例如，考虑以下 JavaScript 代码:

```
function add(x, y) {
    return x + y;
}
const result = add(1, "2");
```

在这段代码中，add 函数应该将两个数字相加，但是因为 JavaScript 是一种动态类型的语言，所以它会默默地尝试将字符串“2”转换为一个数字，然后将其加到 1，这将产生错误的结果。这可能很难调试，尤其是在大型复杂的代码库中。

# 带类型的函数

使用 TypeScript，我们可以向 add 函数添加类型注释，以指定它接受两个数字作为参数并返回一个数字:

```
function add(x: number, y: number): number {
    return x + y;
}
const result = add(1, "2"); // This will cause an error
```

现在，如果我们试图将一个字符串作为第二个参数传递给 add 函数，TypeScript 编译器会给我们一个错误，提醒我们代码中有一个 bug。这可以为我们节省大量的时间和挫折，它可以帮助确保我们的代码是正确的，没有错误。

TypeScript 之所以重要的另一个原因是，它提供了许多普通 JavaScript 所不具备的特性。例如，TypeScript 支持类、接口和模块，这可以帮助我们以更具逻辑性和可维护性的方式组织代码。它还支持类型推断，可以根据变量和表达式使用的上下文自动推断它们的类型。这可以节省我们大量的时间和精力，并且可以使我们的代码更加简洁，可读性更好。

总的来说，TypeScript 是编写优秀的、可读的 JavaScript 代码的一个有价值的工具。它允许我们向代码中添加类型注释，这有助于防止错误并使代码更容易理解。它还提供了许多普通 JavaScript 中没有的附加特性，可以帮助我们编写更加模块化和可维护的代码。如果您正在从事一个大型或复杂的 JavaScript 项目，那么使用 TypeScript 绝对是值得考虑的。

# 谢谢！

![](img/34b6d4e88daa5f22c87d2b9b476f66e5.png)

读完这个故事后，我希望你学到了一些新的东西，或者受到启发去创造一些新的东西！🤗

如果我给你留下了问题或一些要说的话作为回应，向下滚动并给我键入一条消息。如果你想保密，请在 Twitter @DevByRayRay 上给我发一条 [DM。我的 DM 永远是开放的😁](https://twitter.com/@devbyrayray)

[**通过电子邮件获取我的文章点击这里**](https://byrayray.medium.com/subscribe) **|** [**购买 5 美元的中等会员资格**](https://byrayray.medium.com/membership)

## 阅读更多

![RayRay](img/992af170033696163d6cc0269218aedd.png)

[雷雷](https://byrayray.medium.com/?source=post_page-----c6561b70a34b--------------------------------)

## 最新的 JavaScript 和 TypeScript 故事

[View list](https://byrayray.medium.com/list/latest-javascript-typescript-stories-0358ad941491?source=post_page-----c6561b70a34b--------------------------------)14 stories![](img/c93ca03b33796c40dcc47873de2697c2.png)![](img/86f37efa11855f6f0f0f62984c37f696.png)![](img/ddbaa6d0bea676316247e82043d60b63.png)

## 你是否希望为你的软件创业增加知名度？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费每周简讯**](http://newsletter.plainenglish.io/) 。关注我们关于 [**推特**](https://twitter.com/inPlainEngHQ)[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，以及** [**不和**](https://discord.gg/GtDtUAvyhW) **。****