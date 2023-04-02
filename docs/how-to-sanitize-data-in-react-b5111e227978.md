# 如何整理 React 中的数据

> 原文：<https://javascript.plainenglish.io/how-to-sanitize-data-in-react-b5111e227978?source=collection_archive---------4----------------------->

## 关于如何利用 TypeScript 在 React 应用程序中整理数据的教程

![](img/837d4e2d64a04621843a9514abee62f4.png)

Photo by [Tobias Fischer](https://unsplash.com/@tofi?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/clean-data?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

每个现代 ReactJS 应用程序都以某种方式处理数据。我们获取数据，并让人们在整个应用程序中与之交互。

但是，如果我们不小心什么数据进入我们的网站，它可能会导致我们的应用程序失败。

> 应用程序在运行时崩溃的主要原因之一是坏数据。

今天，我们将看到一种在 React 应用程序中净化数据的方法。

# 问题是

你不应该相信任何人。也许您希望远程 API 返回如下所示的数据。

userData.ts

您有一个组件，它以下面的方式显示这两段数据。

SomeComponent.tsx

现在出于某种原因，后端的开发人员想，好吧，让我们稍微改变一下数据的结构，使其更加扁平，并将其改为

changeUserData.ts

现在，一旦他们这么做了，你的应用程序就会在运行时失败，因为它不知道结构已经被改变了。

您将返回到桌面并解决问题，但是您的用户将会看到一个崩溃的应用程序。

```
Error: Cant't read name of undefined
```

避免这种事故的一个方法是

```
<div> {user?.basicInfo?.name} </div>
```

但是你必须把这些标志放在不干净的地方，对吗？

# 利用 Typescript。

现在让我们像下面这样定义我们的用户模型

UserInterface.ts

所以这个`**initUser**`方法可以用来创建一个用户实例，并且如果我们需要的话，`options`参数使得传递参数变得很容易。

如果我们不传递任何东西，我们会用默认值取回对象。

因此，在将数据推入组件之前，您将通过`initUser`方法传递数据并保持冷静。

或者你可以用钩子。

useCleanUserData.ts

这样，我们就不需要担心 API 数据是否干净了。

您也可以对 redux 使用相同的方法。利用`selectors`，以便数据在进入组件之前被清理。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****