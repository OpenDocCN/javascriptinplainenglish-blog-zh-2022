# 您可能已经错过的 4 个 React 本地库

> 原文：<https://javascript.plainenglish.io/4-more-react-native-libraries-you-might-have-missed-41abe79b27ec?source=collection_archive---------5----------------------->

![](img/0c335192fe94920a4508223a9f963d77.png)

Photo by [Susan Q Yin](https://unsplash.com/@syinq?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一年前，我分享了 5 个我个人觉得有用的 React 原生库。它也受到了很多读者的欢迎。如果你以前没有看过，你可以在这里查看一下。今天，我很高兴再分享其中的 4 个！

像往常一样，向所有的个人贡献者大声欢呼，因为他们创造了所有这些令人惊叹的库。作为 React 本地开发人员，让我们通过主演、分享，最重要的是在您的项目中采用它们来表达我们的爱。

# 1.默蒂

默蒂本质上是反应本地版本的[制定者议案](https://www.framer.com/motion/)。它是在**“一次编写，随处动画化”**的口号下创建的。这意味着你可以在网上分享你的原生应用动画，例如，如果你正在使用 [React Native Web](https://github.com/necolas/react-native-web) 。

默蒂有令人难以置信的表现，因为它使用了引擎盖下的[复活 2](https://docs.swmansion.com/react-native-reanimated/) 。以前使用过 Framer Motion 的人应该对这些 API 很熟悉。即使对新手来说，默蒂的声明性质也应该是直观的。

有时候我发现 Reanimated 或者传统的动画 API 让人望而生畏。有了默蒂，更容易快速构建高性能的动画。

[](https://moti.fyi/) [## 欢迎来到默蒂|默蒂

### 默蒂是由费尔南多·罗约制作的 React Native 的通用动画包。通用:适用于所有平台 60…

moti.fyi](https://moti.fyi/) 

# 2.反应本地 MMKV

这实质上是异步存储的高性能替代产品。它是用 C++写的，用 JSI 代替了旧的桥。

您可以自定义存储位置并加密您的数据。但这需要深入研究原生 iOS 或 Android 库代码。

[](https://github.com/mrousavy/react-native-mmkv) [## github-mrousavy/react-native-mmkv:⚡️react native 最快的键/值存储。大约快 30 倍…

### MMKV 是微信开发的一个高效的小型移动键值存储框架。更多见腾讯/MMKV…

github.com](https://github.com/mrousavy/react-native-mmkv) 

# 3.React Native BlurHash

这个库在加载图像时提供了模糊的占位符。与使用灰度骨骼相比，它提供了更加丰富多彩的加载体验。

这是网络行业的趋势。我们可以看到像 Next 和 Gatsby 这样的框架，以及 Cloudinary 这样的图像管理平台提供了模糊的占位符选项。看到更多的移动应用程序被采用将是令人高兴的。

[](https://github.com/mrousavy/react-native-blurhash) [## github-mrousavy/react-native-blur hash:🖼️一个库，用于显示彩色模糊占位符，同时…

### 🖼️为您的用户提供他们想要的装载体验。通过 npm 安装:NPM I react-native-blur hash npx pod-install…

github.com](https://github.com/mrousavy/react-native-blurhash) 

# 4.反应原生视觉相机

这可能是最好的相机库了。从相机类型到拍摄格式，您拥有构建基于相机的应用程序所需的所有控件。

最引人入胜的功能是**帧处理器**。这是一个处理摄像机捕捉到的东西的功能。它允许我们创建高级功能，如人工智能面部和物体识别，条形码扫描仪，Instagram 类过滤器等。它们以用本地代码编写的插件的形式出现。

[](https://mrousavy.com/react-native-vision-camera/) [## 来自 VisionCamera | VisionCamera 的问候

### 📸看到视觉的相机库。VisionCamera 的设计初衷是提供所有功能和…

mrousavy.com](https://mrousavy.com/react-native-vision-camera/) 

# 思想

完成写作后，我意识到两件事:

1.  [马克·鲁沙维](https://github.com/mrousavy)是一个创造了 3 个图书馆的野兽🙌
2.  所有这些图书馆都在利用 JSI

React Native 在性能上一直饱受诟病。看到范式向 JSI 转移令人兴奋，这将震撼 React 原生应用的整体性能。

[](https://medium.com/@fabianlee/membership) [## 通过我的推荐链接加入 Medium-Fabian Lee

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@fabianlee/membership) 

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*