# 如何使用 Expo 创建 React 本地视频播放器

> 原文：<https://javascript.plainenglish.io/how-to-create-react-native-video-player-using-expo-downloadable-project-included-feaa78c0db60?source=collection_archive---------4----------------------->

## 使用 Expo 创建 React 原生视频播放器所需的一切。

在本文中，我们将从头开始讲述如何在 React 原生跨平台上创建一个简单的视频播放器，该播放器将使用 Expo 在 Android 和 IOS 操作系统上播放视频。

![](img/e5f8ecf3b139413f396928fdd300df58.png)

# 创建世博项目

让我们使用 Expo CLI 创建一个新项目，方法是在终端中键入下一个命令(首先检查您是否在您想要的当前路径中):`**expo init video-player**`。该命令将询问您想要什么类型的项目，空白 JavaScript 还是空白 TypeScript，在本文中，我将选择空白 TypeScript。现在我们等待几秒钟，我们的 Expo 项目就可以开始工作了。

安装完成后，打开终端，运行下一个命令，用 Android/IOS 模拟器运行项目。`**expo start**`命令将向您显示一个带有运行项目选项的菜单，并选择您的模拟器偏好:“a”用于 Android，“I”用于 IOS。选择之后，模拟器将构建并运行项目。

![](img/e31ba579c333c6bdcc6c53fae4fada15.png)

Project Done With React Native & Expo

# 视频组件安装

创建项目后，我们现在可以导入视频组件。视频组件是来自`**expo-av**`的一个组件，它在你的应用程序中显示与其他 UI 元素一致的视频，所以要使用视频组件，我们应该先安装`**expo-av**` 。在项目根路径中打开终端，键入下一个命令:`**expo install expo-av**`。这将把库导入到我们的项目依赖项中。

# 准备

在使用之前，让我们打开 App.tsx 文件，您应该会看到下面的代码行:

```
export default function App() {
  return (
    <View style={styles.container}>
      **<Text>Open up App.tsx to start working on your app!</Text>
      <StatusBar style="auto" />**
    </View>
  );
}
```

现在删除选中的粗体代码行。在视图标签中，我们将创建我们的视频播放器。

# 使用

首先，我们从`**expo-av**`导入视频组件。

```
import { Video } from "expo-av";
```

现在我们可以在代码中使用视频组件了。我们将在视图标签中定位视频组件，但是在此之前，我们有一些视频组件**需要**提供的道具。

# **所需道具**

## 源道具

我们需要提供给视频组件的源是我们想要在播放器中播放的视频的路径。该路径将作为 URI 放入源代码中，如下所示:

```
<Video
  **source**={{
    **uri**: "[http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4](http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4)",
  }}
/>
```

## **风格道具**

风格道具很重要，因为如果我们不提供它，我们将根本看不到玩家，所以我们需要设置玩家的宽度和高度，并将其居中，如下面的代码所示:

```
<Video
  **style={styles.video}**
  source={{
    uri: "[http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4](http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4)",
  }}
/>**//STYLE**
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
  video: {
    alignSelf: 'center',
    width: 320,
    height: 200,
  },
});
```

通过这些步骤，我们已经可以看到视频播放器并播放我们在 URI 提供的视频。

但是现在，我将继续设置一些可选的道具，在我看来，知道这些道具非常重要。

# 可选道具

## 调整模式道具大小

有了这个属性，我们可以描述视频应该如何缩放以在组件视图边界中显示。必须是下列值之一:

*   包含(contain )-在保持纵横比的同时，在元件边界内进行调整。
*   覆盖(cover )-填充元件边界，同时保持纵横比。
*   拉伸(Stretch )-拉伸以填充元件边界。

我通常在**中使用**模式。

```
<Video
  style={styles.video}
  **resizeMode**="contain"
  source={{
    uri: "[http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4](http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4)",
  }}
/>
```

## 使用本地控件属性

一个布尔值，如果设置为`true`，将在`Video`组件中显示本地回放控件(如播放和暂停)。

```
<Video
  style={styles.video}
  resizeMode="contain"
  source={{
    uri: "[http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4](http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4)",
  }}
  **useNativeControls**={true}
/>
```

## 正在循环道具

一个布尔值，描述视频应该播放一次(`false`)还是无限循环(`true`)。

```
<Video
  style={styles.video}
  resizeMode="contain"
  source={{
    uri: "[http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4](http://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4)",
  }}
  useNativeControls={true}
  isLooping={true}
/>
```

## 海报源道具

加载视频时，视频组件根本不会显示，直到视频完全加载。您可以在视频加载时显示一个图像，让用户知道他需要等待几秒钟才能完全加载。非常有用。

在视频组件中还有更多有用的道具没有在这里介绍，但是您已经有了一个基本的视频播放器，它可以播放来自本地手机存储和网络的视频，还包括一些其他功能。

如果你想了解更多关于视频组件道具的信息，你可以点击这里查看:

[](https://docs.expo.dev/versions/v44.0.0/sdk/video/) [## 视频博览会文件

### 中的视频组件将视频与应用程序中的其他 UI 元素内联显示。许多视频和音频都有…

docs.expo.dev](https://docs.expo.dev/versions/v44.0.0/sdk/video/) 

完整的项目可以从这里下载: [***链接***](https://github.com/nissimzarur/video-player.git)

**感谢您的阅读。**请关注我，为所有需要的人鼓掌/评论助推这篇文章。

**感谢您到目前为止的阅读，如果您喜欢这样的内容，并且您想支持我作为一名程序员和作家撰写更多这样的文章， [***请使用我的链接注册 Medium 成为会员(每月订阅 5 美元)，您将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*