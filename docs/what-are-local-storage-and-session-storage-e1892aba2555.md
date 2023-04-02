# 什么是本地存储和会话存储？

> 原文：<https://javascript.plainenglish.io/what-are-local-storage-and-session-storage-e1892aba2555?source=collection_archive---------10----------------------->

## 本地存储和会话存储之间的区别，以及如何使用它们的示例。

![](img/d9da8c5024708ecbde160818ccc9e27f.png)

Photo by [Scott Graham](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您是 web 开发人员，那么您可能听说过本地存储和会话存储。但是它们到底是什么呢？而这两者的区别是什么？在这篇博文中，我们将讨论本地存储和会话存储之间的区别，并提供如何使用它们的示例。

## Web 存储 API

在 HTML5 之前，开发人员只能依靠 cookies 在客户端存储数据。然而，当 HTML5 推出时，开发人员可以选择使用一种叫做 Web Storage 的新 API。这个 API 提供了两种不同类型的存储:本地存储和会话存储。本地存储和会话存储允许 web 应用程序在用户的浏览器上本地存储数据。

## 会话存储

会话存储是一种 web 存储，只允许在当前会话期间将数据存储在客户端。一旦用户关闭浏览器，存储在会话存储中的所有数据都将被删除。

会话存储对于存储不需要跨会话保持的临时数据很有用，例如会话 id 或仅在当前会话期间使用的临时数据。

## 在会话存储中设置数据

要在会话存储器中设置数据，可以使用`setItem()`方法。该方法接受两个参数:

*   键，这是一个将用于标识数据的字符串。
*   值，即要存储的数据。

例如，要将名为 user_id 的会话变量设置为值 1234，您需要执行以下操作:

```
sessionStorage.setItem(‘user_id’, ‘1234’);
```

## 从会话存储中检索数据

要从会话存储中检索数据，可以使用`getItem()`方法。此方法接受单个参数，该参数是您要检索的数据的键。例如，要获取 user_id 会话变量的值，您需要执行以下操作:

```
let user_id = sessionStorage.getItem(‘user_id’); // 1234
```

## 从会话存储中删除数据

要从会话存储中删除数据，可以使用`removeItem()`方法。此方法接受单个参数，该参数是要删除的数据的键。要删除 user_id 会话变量，您需要执行以下操作:

```
sessionStorage.removeItem(‘user_id’);
```

![](img/e20fbba8469e6c1742dcbaae6b6d61a0.png)

Photo by [ThisisEngineering RAEng](https://unsplash.com/@thisisengineering?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 局部存储器

本地存储是一种 web 存储，它允许数据无限期地存储在客户端。与会话存储不同，即使在浏览器关闭后，存储在本地存储中的数据仍然存在。

本地存储对于存储需要跨会话保持的数据很有用，例如用户首选项或设置。

## 在本地存储中设置数据

要在本地存储器中设置数据，也可以使用`setItem()`方法。该方法接受相同的两个参数:

*   键，这是一个将用于标识数据的字符串。
*   值，即要存储的数据。

使用相同的示例，我们可以将名为 user_id 的局部变量设置为值 1234。

```
localStorage.setItem(‘user_id’, ‘1234’);
```

## 从本地存储中检索数据

要从本地存储中检索数据，您也可以使用`getItem()`方法。该方法接受同一个参数，这是您想要检索的数据的键。

```
let user_id = localStorage.getItem(‘user_id’); // 1234
```

## 从本地存储中删除数据

要清除本地存储中的所有数据，可以使用`clear()` 方法。此方法不接受任何参数。

```
localStorage.clear();
```

要从本地存储中删除特定的项目，您可以使用`removeItem()`方法。此方法接受单个参数，该参数是要删除的数据的键。

```
localStorage.removeItem(‘user_id’);
```

## 本地存储与会话存储

既然我们已经介绍了本地存储和会话存储的基础知识，那么让我们来讨论两者之间的区别。

本地存储和会话存储的主要区别在于，存储在本地存储中的数据即使在浏览器关闭后仍然存在，而存储在会话存储中的数据仅在当前会话期间可用。

另一个区别是本地存储不是基于会话的，这意味着本地存储中的数据必须手动删除。最后，本地存储的存储容量也大于会话存储。

本地存储最适合用于需要跨会话保持的数据，如用户首选项或设置。会话存储更适合于会话结束后不需要保存的临时数据。

我希望这篇文章能消除你的任何困惑！祝你的编码项目好运！

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*