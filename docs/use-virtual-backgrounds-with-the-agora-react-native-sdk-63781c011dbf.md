# 通过 Agora React Native SDK 使用虚拟背景

> 原文：<https://javascript.plainenglish.io/use-virtual-backgrounds-with-the-agora-react-native-sdk-63781c011dbf?source=collection_archive---------22----------------------->

![](img/a026a1e7932eac93995900ee5ec28ab9.png)

Agora React Native SDK 现在支持使用虚拟背景。你可以使用纯色或者选择一张图片作为背景。我们将了解如何将图像资源与 React Native 捆绑在一起，以及如何选择用户图像作为虚拟背景。

# 先决条件

*   一个 Agora 开发者账号(免费！[在这里报名](https://sso.agora.io/en/signup?utm_source=medium&utm_medium=blog&utm_campaign=use-virtual-backgrounds-with-the-agora-react-native-sdk)
*   对 React Native 的基本理解

为了让我们快速了解基本的视频通话应用，让我们使用这个[演示](https://github.com/EkaanshArora/Agora-RN-Quickstart)。您可以按照自述文件中的说明让应用程序在您的设备上运行。我们将讨论使用虚拟背景的代码。你可以在 [GitHub](https://github.com/EkaanshArora/Agora-RN-VirtualBackground/) 上找到这个演示的源代码。

我们需要两个开源库:react-native-image-picker 和 react-native-fs。您可以通过执行`npm i --save react-native-image-picker react-native-fs`将它们添加到项目中

# U **唱虚拟背景**

Agora SDK 让它变得非常简单:你只需要用你的配置调用`engine`对象上的`enableVirtualBackground`方法来启用这个特性。你不必担心分割或背景去除之类的事情。

我们将在名为`virtualSource`的`App`类上定义一个属性来创建和存储我们的配置。我们将在状态中添加一个 waiting boolean，这样我们就可以在执行异步代码时禁用 start call 按钮。

我们可以定义一个函数`useColor`，它使用`Color`类构造函数来创建一个颜色对象，该对象使用传递的红色、绿色和蓝色值(颜色范围是`0 — 255`)。然后我们可以更新`virtualSource`属性和我们的状态。

## 使用背景模糊

为了使用背景模糊，我正在创建一个函数`useBlur`。我们可以将`backgroundSourceType`设置为`Blur`并将`blur_degree`定义为所需的强度，我选择的是`Medium`。

## 捆绑资源以用作虚拟背景

要捆绑图像，可以将其复制到项目目录，并使用所需的语法引用它。在使用 RNFS 测试时，我们可以使用 URI 下载映像。然后，我们可以用图像的绝对路径更新配置的 source 属性。

## 使用用户图像作为虚拟背景

我们可以使用`react-native-image-picker`中的`launchImageLibrary`来访问图像 URI。我们处理基于操作系统的映像访问，并将映像的绝对路径传递给配置文件。

最后，我们可以在加入频道之前更新我们的`startCall`功能来启用虚拟背景:

# 结论

借助 Agora SDK 和开源库，您可以非常轻松地为视频通话和直播添加虚拟背景。你可以在 [API 参考](https://docs.agora.io/en/Video/API%20Reference/react_native/index.html)中找到其他很酷的特性。你可以在这里阅读如何用几行代码[构建一个视频通话应用。](https://www.agora.io/en/creating-a-react-native-video-chat-app-in-a-few-lines-of-code-using-agora-uikit/)

我邀请您[加入 Agora 开发者 Slack 社区](https://www.agora.io/en/join-slack/)。欢迎在`#react-native-help-me`频道提出任何关于该项目的问题。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***