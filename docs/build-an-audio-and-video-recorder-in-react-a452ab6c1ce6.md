# 在 React 中构建一个音频和视频记录器

> 原文：<https://javascript.plainenglish.io/build-an-audio-and-video-recorder-in-react-a452ab6c1ce6?source=collection_archive---------3----------------------->

## 如何捕获视频和记录音频，并保存到本地存储器。

![](img/4e617eda3f3bac49fcc377ff9c873d59.png)

Photo by [rupixen.com](https://unsplash.com/@rupixen?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

对于许多应用程序来说，使用浏览器应用程序录制音频和视频是一个相当常见的用例。尤其是笔记应用。

为了实现这些特性，我们已经有了一个名为 [recordrtc](https://www.npmjs.com/package/recordrtc) 的不错的库。让我们看看如何在 React 应用程序中使用它。

# 安装依赖项

首先，安装依赖项。

```
yarn add recordrtc
```

# 获得许可

为了使用 React 应用程序录制音频或视频，您必须获得用户的许可。

我们的 recordrtc 库让这一切变得简单。只需创建一个函数来获取权限并初始化记录器的实例。

permission

我们甚至可以把它做成可重复使用的挂钩。

hook for permission

注意我们在钩子内部传递了一个`recordingType`参数。这将决定我们是否试图记录音频或视频或其他东西。

我们可以像这样在组件内部使用它。

```
const recorder = useRecorderPermission("audio");
```

# 来录音吧！

现在我们有了一个钩子，它从用户那里获得许可，启动一个记录器对象，并把它返回给我们。

让我们写两个函数来开始和停止记录。

注意，我们正在使用我们的记录器`startRecording`和`stopRecording`功能。我们还从名为 invokeSaveAsDialog 的库中获得了一个额外的函数，它允许我们指定要保存的文件的名称。

# 使用计时器记录。

假设您想要录制特定时间段的录像。每当点击一个按钮时，您希望记录 20 秒钟的录像。您可以使用下面的代码来做到这一点。

注意我们是如何通过从父节点传递一个属性来定制文件名的。此外，您还可以看到录像剩余的秒数。

# 显像记录

如果你想录制一段屏幕的视频，那么只需通过我们的`useRecorderPermission`钩子里面的`video`而不是`audio`，就可以了！

就是这样。我希望你今天学到了新东西！

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

## Github 资源库:

[](https://github.com/Mohammad-Faisal/react-audio-video-record-demo) [## GitHub-Mohammad-fais al/react-音频-视频-记录-演示

### 使用浏览器应用程序录制音频和视频是许多应用程序的常见用例。尤其是…

github.com](https://github.com/Mohammad-Faisal/react-audio-video-record-demo) 

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*追随我们。查看我们的* [***社区不和***](https://discord.gg/GtDtUAvyhW) *并加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*