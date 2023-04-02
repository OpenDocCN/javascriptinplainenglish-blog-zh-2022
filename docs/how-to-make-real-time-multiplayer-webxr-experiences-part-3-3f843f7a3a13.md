# 如何打造实时多人 WebXR 体验——第 3 部分

> 原文：<https://javascript.plainenglish.io/how-to-make-real-time-multiplayer-webxr-experiences-part-3-3f843f7a3a13?source=collection_archive---------8----------------------->

## 使用 Websockets、React Three Fiber 和 DynamoDB 允许多个用户在 WebXR 中与 3D 模型进行交互。

![](img/d771908d1ec465f98573e480557a4006.png)

# 介绍

这是第三篇详细介绍如何制作实时多人 WebXR 体验的博文。

已经涵盖了如何工作的概念方面和如何实现用户位置数据的实践方面，这篇博文将阐明如何实现与 3D 模型的交互，以便用户可以实时地与他们的环境交互。

如果你还没有，请阅读上面提到的另外两篇文章，并愉快地阅读下面的:D

# 代码示例

在[之前的博文](https://jamesmiller.blog/how-to-make-real-time-multiplayer-webxr-experiences-part-2/)中，我谈到了在索引目录中声明的 XRScene 高阶组件(HOC)。

我们将从这里开始，并扩展到:

1.  如何声明一个 3D 模型
2.  如何让这些 3D 模型互动
3.  如何将 Websockets 与 3D 模型集成

我们走吧，:D

## 如何声明 3D 模型

为了使用 Websockets 发出和检索 3D 模型的位置数据，您需要首先实例化 Websockets(如本系列教程的第 2 部分所述),然后声明一个用于利用这些 Websockets 的 3D 模型组件。

让我们先看看 index.js 文件，看看我是如何设置它们的。

**index . js 文件**

请参见第 8 行和第 20–24 行，它们显示了 3D 模型的加载位置。

您可以看到，我们正在将名称、位置和旋转属性传递给这个组件——让我们更仔细地看看 Shiba.js 组件，以了解它们是如何被使用的。

**三维模型组件(Shiba.js)**

该组件负责渲染 GLTF 3D 模型，允许它与 XR 控制器交互，并将其连接到 Websockets。

为了进一步细分:

*   **渲染 GLTF 模型**:第 16–32 行之间是由[开源库自动生成的逻辑，该库将 gltf 转换成 React-Three-Fiber 组件](https://github.com/pmndrs/gltfjsx)。
*   **为模型启用 XR 交互性**:在第 12 行和第 39 行，带有 XrInteractivity.js 的高阶组件(HOC)用于为 Shiba.js 提供 XR 交互性。
*   **为模型启用 web sockets:**在第 11 行和第 40 行，HOC withCollaboration.js 用于为 Shiba.js 提供。

## 如何让这些模型互动

为了能够使用你的 XR 控制器(例如 Oculus Quest 2 控制器或 HoloLens 2 手动跟踪控制器等)，你需要实现一个名为 react-three/xr 的库。

在本例中，我已经在一个名为 withXrInteractivity.js 的特设中实现了这一点，让我们更深入地了解一下！

**高阶组件— withXrInteractivity.js**

该特设委员会负责:

*   **使 xr 控制器能够“抓取”对象:**第 40–46 行我们使用 react-three/xr 提供的 RayGrab HOC，用于能够进行 XR 交互的设备。
*   **跟踪被移动的模型的位置值:**第 18–26 行我们使用 react-three/xr 中的 useXREvent 函数来跟踪物体移动的位置。
*   **使用已移动对象的名称和位置更新全局应用程序状态:**最后，在第 28–36 行之间，我们计算出附加了此 HOC 的哪些对象已被移动，然后使用该对象的名称和位置值更新应用程序的全局状态。

## 如何将 Websockets 与 3D 模型集成

一旦我们使模型与 XR 控制器交互，我们就需要集成 WebSockets 的使用，以允许其他用户看到您移动的模型的新位置。

这需要理解两个方面，第一个是负责前端实际 Websocket 集成的 **withCollaboration.js** HOC，第二个是 DynamoDB 中数据的实际样子。

**高阶组件— withCollaboration.js**

从前端开始，withCollaboration.js 执行以下操作:

*   **将您刚刚使用 XR 控制器移动的对象的位置提交给 Websocket** :第 19–25 行检查您的设备是否能够进行 XR 交互，如果能够，它将使用正在移动的模型的名称、移动的模型的位置以及移动它的用户的名称来更新 Websocket
*   **监听 Websocket 的任何更新，并更新移动模型的位置**:第 28–32 行监听 Websocket 上的更新，然后检查提交它的用户是否与提交它的用户不同，如果是，那么模型的新位置被应用到场景。

在最后一点的基础上，它需要检查提交运动的用户是否与在 web 应用程序上接收位置数据的用户不同的原因是为了防止最初提交模型新位置的用户的位置值反弹。

例如，如果您向 Websocket 提交位置值，Websocket 会立即检测到您移动了模型，并尝试更新您刚刚移动的模型的位置——这可能会在三个位置处造成混淆。JS 层，并导致模型的位置移动不稳定，并成为错误。

【WebSocket 位置数据的数据库

将模型的新位置值提交给 Websocket 后，通过本系列教程第 2 部分中概述的相同过程，将该值传递给 DynamoDB。

我在下面附上了 DynamoDB 表的截图，其中显示了两种类型的条目:**对象**和**用户**。

**用户**指已经登录并四处移动的人，他们的位置值存储在那里(见本教程系列的第 2 部分)。

**对象**指的是用户使用他们的 XR 控制器移动的模型，如本文所述，让我们更深入地了解一下。

![](img/2b24a4c92b072bf0636c7554d2297d8d.png)

Screenshot of the positional data in the DynamoDB Table

查看存储的模型条目的示例，您可以看到存储了模型的名称(在本例中为“shiba”)以及模型的位置(称为“matrixWorld”)和提交新位置的用户的名称。

我们将位置存储为“矩阵世界”而不是 x/y/z 值的原因是，当您使用 XR 控制器移动模型时，模型的位置会发生复杂的变化。

当您使用 XR 控制器“抓取”一个模型时，该模型将成为控制器的子模型，直到您释放该模型。

为了向其他用户提供您将模型移动到的准确位置，我们存储了模型的“matrixWorld”位置，这实际上是它的全局位置，而不是它相对于 XR 控制器的位置(也就是说，不是它作为 XR 控制器的子节点的位置)。

# 结论

这是大量的信息！

我真的希望这有助于你使用 React-Three-Fiber 和 Websockets :D 进行实时多人 WebXR 体验

幸运的话，您将能够为您的应用程序改编这些代码——或者更好地使用 [Wrapper.js](https://github.com/JamesMillerBlog/wrapper.js) 来构建您的 WebXR 体验！

我希望这能有所帮助，同时，祝你在:D 玩得开心

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***