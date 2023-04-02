# React —通用容器

> 原文：<https://javascript.plainenglish.io/react-universal-container-acfc138ccfef?source=collection_archive---------7----------------------->

## 创建一个可重用的容器来加载多个表示组件的数据

![](img/6040d52d732979182aafc7e5543599c9.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你用 React 编码，你一定听说过容器组件，并以某种形式使用过它们。简而言之，容器组件:

*   都是关于功能性的。
*   向它们的孩子提供数据和行为——通常是表示性组件——因此，通常是有状态的。
*   除了包装`<div>`或反应片段`<>`之外，很少有自己的标记。

正确使用时，容器组件实现了[关注点分离](https://en.wikipedia.org/wiki/Separation_of_concerns) (SoC)设计模式。它们从组件中抽象出数据处理逻辑，从而将功能与外观分开。

虽然容器组件的常见用法——将数据传递给表示组件——对于大多数场景来说已经足够了，但我很高兴了解到如何创建一个可重用的容器来为多个表示组件加载数据。结果是减少了代码并简化了可维护性。

我们开始吧！

# 先决条件

请注意这篇文章:

*   要求中级精通 React 概念，特别是状态、钩子和子对象。如果你是初学者，这篇文章仍然是有价值的，但不解释上述主题。
*   不包括容器和表示组件，它们是什么，以及何时使用它们。同样参考[这篇](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)文章。
*   特性 [GitHub 的用户 API](https://docs.github.com/en/rest/reference/users) 和 gists 中的[动物园动物 Api](https://zoo-animal-api.herokuapp.com/) 。

让我们通过查看容器组件的常见用例来获得一些上下文。然后，我们将重构容器组件，直到我们达到期望的结果。

# 普通集装箱

假设我们需要在应用程序中显示特定用户的详细信息，容器组件获取用户数据并将其传递给呈现该数据的组件。因此，我们需要创建以下内容:

1.  表象成分:`User`
2.  集装箱组件:`UserContainer`

## 表象成分

首先，我们有表示组件`User`，它呈现传递给它的细节。

User.js

## 容器组件

然后，我们创建容器组件`UserContainer`。

UserContainer.js

最后，将以上所有内容放在一起的`App.js`文件看起来像这样:

App.js

这是容器组件模式的完美版本。然而，想象一下，我们也需要我们的应用程序来显示用户宠物的详细信息。我们如何着手做这件事？

基于上述实现，我们需要创建两个组件:

1.  表象成分:`Pet`
2.  容器组件:`PetContainer`

因此，每个基于数据获取功能的新模块都需要两个组件。不用说，维护一段时间后就变得繁琐了。我们可以通过重构容器组件来获取数据并将所述数据传递给任何组件，从而缓解这个问题。在我们这样做之前，让我们修改`UserContainer`使其更加动态。

# 改进的容器

重构后的容器组件如下所示:

UserContainer.js

您可以看到，除了`return`块(奇迹发生的地方)，我们的容器组件保持不变。在讨论重构带来了什么变化以及在`return`块中发生了什么之前，我们先来看看存放改进后的容器的`App.js`文件。

App.js

在`App.js`中，我们将`User`包装在`UserContainer`中，而不是像以前那样只调用`UserContainer`。为了理解为什么，让我们回到容器的`return`块，并遍历它的步骤:

UserContainer.js

1.  `[React.Children.map](https://reactjs.org/docs/react-api.html#reactchildrenmap)`对包含在`props.children`中的每个直接子节点调用一个函数。
2.  `[React.isValidElement](https://reactjs.org/docs/react-api.html#isvalidelement)`是一个布尔函数，用于验证对象是否为 React 元素。
3.  `[React.cloneElement](https://reactjs.org/docs/react-api.html#cloneelement)`克隆有效的 React 元素并返回新的元素。结果元素将原始元素的道具与新的道具进行了浅层合并。

将上述内容应用到我们的代码中:

1.  `UserContainer`克隆`User`组件并返回一个新的`User`组件。
2.  新的`User`组件包含与其现有道具浅合并的道具`user`(在这种情况下没有现有道具)。

因此，在运行时，`UserContainer`中的`return`块产生:

```
return <User user={user} />
```

总而言之，我们重构的容器将数据传递给表示组件，而不需要导入所述组件。

太好了！我们离最终解决方案又近了一步。

# 通用集装箱

为了使我们的容器可以被多个表示组件重用，我们需要:

*   将数据提取 URL 和属性名从容器中分离出来。我们可以通过将道具名称(`resourceName`)和数据获取 URL ( `resourceUrl`)作为道具传递给容器来实现。
*   修改状态变量名称，使其通用。我要用`data`，但是你可以用任何你认为合适的名字。
*   动态设置道具名称如下:
    `{ [resourceName]: data }`

因为我们的容器的主要目的是获取数据，我们可以将其重命名为`FetchData`。完成上述更改后，我们的通用容器将如下所示:

最后，`App.js`文件看起来像这样:

App.js

如上所述，我们可以将容器`FetchData`用于多个表示组件(在本例中是`User`和`Pet`)。

你有它！现在，您知道了如何为共享数据处理逻辑的组件最大化容器组件模式的功效。但是和所有的编码范例一样，根据需求和时间表来权衡你的选择，选出最好的一个。感谢阅读！

# 来源

*   *反应顶级 API，*[https://reactjs.org/docs/react-api.html](https://reactjs.org/docs/react-api.html)
*   *反应容器组件——Learn.co，*[https://learn.co/lessons/react-container-components](https://learn.co/lessons/react-container-components)

*更多内容请看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*