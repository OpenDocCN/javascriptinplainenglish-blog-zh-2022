# 如何结合 Node.js 和 Docker 使用 FFmpeg

> 原文：<https://javascript.plainenglish.io/how-to-use-ffmpeg-with-node-js-and-docker-c21f56993e14?source=collection_archive---------3----------------------->

## 如何轻松处理 Node.js 中的音频和视频文件

![](img/266c32f832bc6a7356cab786cc70fad4.png)

Photo by Donald Tong: [https://www.pexels.com/photo/black-camera-recorder-66134/](https://www.pexels.com/photo/black-camera-recorder-66134/)

今天我们将学习如何在 Docker 容器中使用 FFmpeg 和 Node.js。

# 背景

通常，当我们运行 Node.js 应用程序时，该应用程序所需的所有部分都在 npm 包中，这些包位于 **node_modules** 文件夹中。

然而，对于一些特定的用例，我们需要访问操作系统级的应用程序，这就有点复杂了。

一个很好的例子就是 FFmpeg，在他们的文档中被描述为[:](https://ffmpeg.org/)

> 一个完整的跨平台解决方案，用于录制、转换和流式传输音频和视频。

长话短说，如果你需要与音频和视频转换或修改工作，你会需要这个。

# 问题是

问题是 **FFmpeg** 不是任何你可以安装和使用的 npm 模块。在 **FFmpeg** 之上有一些库，比如`[ffcreator](https://www.npmjs.com/package/ffcreator)`和`[fluent-ffmpeg](https://www.npmjs.com/package/fluent-ffmpeg)`，它们在 FFmpeg 之上创建了一个抽象，但是你仍然需要在操作系统层安装 FFmpeg。

因此，要解决这个问题，一个简单的解决方案是在运行应用程序的服务器上安装 FFmpeg。

但是在现代，我们几乎不直接使用硬件。因为无论何时你需要一个新的服务器，你都需要重新安装它。

哪一个是重复和无聊的？

# 解决方案

更简单的方法是将你的应用程序与安装在 Docker 镜像中的 FFmpeg 捆绑在一起，这使得它非常容易分发，并且你的应用程序现在是可共享和可复制的！

但是你具体是怎么做的呢？真的很简单。在您的基本映像之上，您将运行安装 FFmpeg 的命令，就这样！

下面是一个工作的 does 文件。

Dockerfile

因此，中间的 3 行代码将 FFmpeg 安装到 Node.js Alpine 基础映像中。

```
RUN apk updateRUN apk addRUN apk add ffmpeg
```

注意:我们使用`apk add`是因为在顶部，我们选择了`node:16-alpine`版本的 node(它的尺寸更小)。

如果你使用的是一个合适的 Node.js 镜像，比如`node:16`，那么安装 FFmpeg 的命令如下:

```
RUN apt updateRUN apt install ffmpeg
```

这应该能行。

# 供选择的

上述方法适用于 Node.js 和 Docker 图像。但是如果你想使用 AWS Lambda 或者 Google Cloud 函数来部署你的 Node.js 应用，那么就会产生一些问题。

为了避免这种情况，还有另一种方法。我们可以使用一个名为`[ffmpeg-static](https://www.npmjs.com/package/ffmpeg-static)`的 npm 包。

在您的项目中:

```
npm install --save ffmpeg-static
```

它将下载二进制文件，并将它们存储在`node_modules`文件夹中。从你的应用程序中，你必须指向二进制文件在`node_modules`文件夹中的路径。

您可以通过以下方式获取路径:

```
var pathToFfmpeg = require('ffmpeg-static');
console.log(pathToFfmpeg);
```

然后，您可以将其导出为路径。

```
ENV PATH="/your/path/to/node_modules/ffmpeg-static/bin/linux/x64:${PATH}"
```

这就是你可以实现的方式。这条特殊的线索很有用。

今天到此为止。祝您愉快！

```
**Want to Connect?**You can reach out to me via [**LinkedIN**](https://www.linkedin.com/in/56faisal/) or my [**Personal Website**](https://www.mohammadfaisal.dev/blog)
```

## 资源:

[](https://stackoverflow.com/questions/50693091/ffmpeg-install-within-existing-node-js-docker-image) [## 在现有 Node.js docker 映像中安装 ffmpeg

### 我需要在 docker 容器(使用 docker-compose 创建)中运行的 Node.js 应用程序中使用 ffmpeg。我非常…

stackoverflow.com](https://stackoverflow.com/questions/50693091/ffmpeg-install-within-existing-node-js-docker-image) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*