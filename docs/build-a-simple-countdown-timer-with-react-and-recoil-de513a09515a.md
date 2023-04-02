# 建立一个简单的反应和反冲倒计时定时器

> 原文：<https://javascript.plainenglish.io/build-a-simple-countdown-timer-with-react-and-recoil-de513a09515a?source=collection_archive---------6----------------------->

## 跨 React 组件共享反冲应用状态的概念验证

![](img/81b4e51004649a3a3be972cf24104e73.png)

(author)

# **背景**

[反冲](https://recoiljs.org/)为前端开发者提供了一个快速学习、易于实现的应用状态管理 API。

关于是否选择这个库而不是其他库作为应用程序状态管理解决方案，已经有了很多写得很好的讨论，但是很难否认设置和使用反冲在不同的 React 组件之间共享状态的简单性。

作为 [DemandStar](https://network.demandstar.com/) 工程团队的一员，我在过去的一年里一直在使用反冲，并且已经看到了我们的代码库在可维护性、可测试性和功能开发的整体速度方面的实质性好处。

在本帖中，我们将通过…展示使用反冲的简易性和有效性

*   构建一个基本的 React 倒计时定时器组件
*   用反冲管理它的状态
*   在几个独立的组件之间共享我们的定时器状态

# 跳到代码

我发现像 [codesandbox.io](https://codesandbox.io) 这样的在线 ide 非常方便地在像 [create-react-app](https://create-react-app.dev/) 这样的环境中剔除组件，引入外部库，甚至将项目附加到源代码控制库或通过免费的测试部署服务实时部署它。

这里是这篇文章完整的[沙箱](https://codesandbox.io/s/recoil-simple-timer-p2gjr)和 [github 库](https://github.com/fauteuil/react-recoil-typescript-simple-timer/)。

# 布局用户界面

首先，让我们设置视图组件。`rrtst-App.tsx`脚本使用[样式组件](https://styled-components.com/)和[类型脚本](https://www.typescriptlang.org/)布局基本视图。

接下来，计时器组件本身驻留在`rrtst-OrangeTime.tsx`中，在这里发生与状态的交互。

这是一个基本的倒计时定时器组件，使用反冲来消耗和保持整个应用程序的状态，并使用`React.useRef`钩子来引用持久定时器对象，使用`React.useEffect`钩子来执行其内部定时器逻辑。

最后，我们包括一个点击处理器来重置反冲状态。

作为一个优化，如果我们想在其他地方重用相同的反冲钩子和定时器逻辑，这在一个 [React 定制钩子](https://reactjs.org/docs/hooks-custom.html)中会更加整洁和可组合。

第 30–42 行在`useEffect`钩子内部有核心逻辑:

*   我们通过一个`setInterval()`调用来分配我们的`timerRef.current`值。React 将跨渲染生命周期持久保存返回的时间间隔 ID，直到我们清除`useEffect`钩子的返回函数中的时间间隔，该函数在组件被卸载时被触发。
*   随着时间间隔每秒重复一次，`orangeTimerState`反冲原子的值会随着递减的值而更新。

这里是`orangeTimerState`原子:

为了在应用程序中的任何地方方便地使用反冲状态，我们有一个简单的只读组件`rrtst-ReadOnlyTimer.tsx`来显示对`orangeTimerState`值的更新。

这个只是订阅了同一个 atom，这导致它在每次更新到倒计时时间间隔时重新呈现。它使用随机颜色值进行样式化，并被放置在主应用程序组件的几个地方，以展示几个组件之间的状态同步性。

所有这些代码都位于我们目录结构的同一层，然而，在现实世界的应用程序中，这一概念使得共享的应用程序状态非常具有性能和可组合性，因为订阅相同反冲原子的子组件可以分布在层次结构的任何一层。

# 结论

很简单，就是这样。感谢阅读！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***