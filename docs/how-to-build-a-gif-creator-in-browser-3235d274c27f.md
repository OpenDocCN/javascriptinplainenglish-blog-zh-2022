# 如何在浏览器中构建 GIF 转换器

> 原文：<https://javascript.plainenglish.io/how-to-build-a-gif-creator-in-browser-3235d274c27f?source=collection_archive---------8----------------------->

## 如何使用 FFmpeg 在浏览器中创建一个简单的 MP4 到高质量 GIF 的转换器？

![](img/35cc51eb8119971422435cb5ff839e28.png)

# 为什么我们还在使用 gif？

gif 拖慢了互联网的速度，因为它们占用了大量的网站存储空间，并且因为将它们推送到客户端所需的总带宽:gif 的重量可能是. mp4 视频文件的 10 倍，并且它们的颜色质量仅限于 256 色调色板。

尽管有这些缺点，Twitter、WhatsUp 和脸书等社交媒体怪物应用程序默认情况下会循环运行 gif，不像用户需要按下播放按钮的视频。这个功能对于内容创作者来说是无价的，可以在第一眼就抓住观众。

如果你想知道 Twitter 和 Telegram 等大型应用程序是如何处理所有这些存储负载的，他们在幕后使用了一个简单而有效的技巧:这些应用程序将胖乎乎的 GIF 文件转换为纤细的 MP4 文件，同时在用户 feed 中显示该文件为未经处理的 GIF 文件。

![](img/54c82780bfed0bf8c3cb6f97508d2f29.png)

# 在线可用转换器

Giphy 是最受欢迎的 GIF 托管提供商，它有自己的 GIF 创建者。IOS 移动应用程序非常好，除了帐户创建是必须的。

[有许多 GIF 编辑器](https://filmora.wondershare.com/animated-gif/best-gif-maker-online.html)运行服务器端 [FFmpeg](https://ffmpeg.org/) 引擎。服务器端方法是常见且可靠的，但有以下缺点:

*   上传用于转换的视频文件可能需要一些时间，具体取决于带宽、视频分辨率和长度。
*   在云上公开运行你的转换器有点昂贵:你需要在一个 [ubuntu 容器](https://stackoverflow.com/questions/50053313/how-to-make-ffmpeg-available-inside-my-docker-container)中为每个客户端运行 FFmpeg 进程，因此当你扩展时，可能会对你的预算有所影响。

我们一直在寻找一种廉价的方式来创建 gif 并在浏览器中处理视频，以节省运行成本和上传费用。过了一会儿，我们发现了一些在浏览器中完成任务的方法:

1.  [**FFmpeg . wasm**](https://ffmpegwasm.netlify.app/)**:**是 FFmpeg 的纯 WebAssembly / JavaScript 端口。它使视频&音频能够在浏览器中录制、转换和流式传输。核心加载速度快约 2 秒，以实现快速互联网带宽，并保持回购。缺点:FFmpeg.wasm 使用 SharedArrayBuffer，这要求站点被隔离。背后的[故事](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer)颇耐人寻味。不幸的是，它在 Safari iOS 上不起作用。
2.  [**GIF shot**](https://yahoo.github.io/gifshot/)**:**是一种不同的方法，通过使用 canvas 分割视频流，从网络摄像头和存储的视频创建 GIF。几年前由雅虎集团创建。不幸的是，它不能在移动 Safari 上工作。

Gifshot Demo

1.  [**video converter . js**](http://bgrins.github.io/videoconverter.js/):也是几年前创建的，使用消息与移植的 FFmpeg 模块通信，该库没有使用 SharedArrayBuffer 方法，因此可以在任何地方工作，包括移动 Safari。它的主要缺点是加载速度:可能需要 5 秒钟来加载内核，并且一些 FFmpeg 过滤器不工作。这是我们基于这种方法构建的一个演示:

VideoConverter.js

# 我们的选择

我们选择了 [FFmpeg.wasm](https://ffmpegwasm.netlify.app/) 来使用普通的 javascript 创建**高质量的 GIF 创建器演示**。

从长远来看，VideoConverter 是一个更好的选择，因为它可以跨平台使用，但它需要一些改造工作来跟上更新的功能。

# 基于 FFmpeg.wasm 构建视频转 GIF 演示

*GitHub 上有完整的代码，你可以把它分叉，按原样部署在*[*Vercel*](https://vercel.com/)*上。*

[](https://github.com/KostaMalsev/high-quality-gif.git) [## GitHub-KostaMalsev/high-quality-gif:浏览器转换器中的视频到 Gif 和 Gif 到视频

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/KostaMalsev/high-quality-gif.git) 

# 循序渐进:

## **第一步:创建 web 应用程序的 HTML 部分**

放置 3 个按钮、图像+视频元素和一个 div“文件”,以便稍后附加处理的输出结果:

## 步骤 2:导入 ffmpeg.wasm 库代码:

定义其全局:

```
<script src="ffmpeg.min.js"></script>
<script>
      //Define ffmpeg:
      const { createFFmpeg } = FFmpeg;
      let ffmpeg;
 </script>
```

您也可以从 cdn 加载更新的库:

```
<script **src="https://unpkg.com/@ffmpeg/ffmpeg@0.10.0/dist/ffmpeg.min.js">**</script>
<script>
      //Define ffmpeg:
      const { createFFmpeg } = FFmpeg;
      let ffmpeg;
 </script>
```

## 步骤 3:为图像/视频加载添加监听器

这里没有实际上传，媒体被格式化到 Uint8Array 缓冲区，使它们可以在 [WebAssembly](https://webassembly.org/) 环境中被 ffmpeg 使用。为此，我们使用*检索图像/视频*功能。

在 Dom 中添加全局变量和对 HTML 元素的引用:

```
var worker;
var sampleImageData = null;
var sampleVideoData = null;
var outputElement;
var filesElement;
var running = false;
var isWorkerLoaded = false;
let fileName = '';**//Get the html elements:** const uploadButtons = document.querySelector('.upload-buttons');
const imageUploadButton = document.querySelector('#image-upload');
const videoTag = document.querySelector("#video-tag");
const inputTag = document.querySelector("#input-tag");
const log = document.querySelector('#log');
const vFigure = document.querySelector('#videoContainer');
const imgTag = document.querySelector('#img-tag');
const button = document.querySelector(".convert-button");
```

## 步骤 4:调用转换 ffmpeg.wasm 引擎

首先用异步函数 *initWorker()* 初始化引擎:

```
//Init the ffmpeg worker
**async function initWorker() {** if (isWorkerLoaded) return; console.log('Start init worker'); ffmpeg = await createFFmpeg({log: true}); button.classList.remove("hidden");
   button.classList.add("gray");
   button.style.setProperty('--load', 0);
   button.innerText = 'Loading engine...'; await ffmpeg.load(); filesElement = document.querySelector("#files");}
```

使用 *convertGifToMp4* 运行 GIF 到 Mp4 转换。

**该部分包括 3 个子步骤:**

1.  通过调用 *ffmpeg 将带有视频数据的 Uint8Array 推送到 w[ASM“file system”](https://emscripten.org/docs/api_reference/Filesystem-API.html)。FS* 以便我们的 FFmpeg 可以读取它。

2.运行 **ffmpeg。使用常规 ffmpeg 指令运行**。

```
**ffmpeg.run('-i', 'input.mp4', '-vf', 'fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse', 'output.gif')**
```

这一行是用 [ffmpeg 标志语言](https://ffmpeg.org/)写的，可以大致翻译成如下:

*使用 input.mp4 文件并将其转换为带有以下标志的 output . gif:*

*设置 fps 为 10(帧每秒)，*

*将输出的高度设置为 320px，宽度设置为原始宽度，使用 lanczos 算法缩放至所需尺寸，*

*使用其中一个输出流生成调色板，选择最佳的 256 种颜色来表示视频中的所有颜色，并在其孪生流上使用该调色板来估计输出 GIF 的颜色。(* [*链接供参考*](https://www.alanwsmith.com/posts/20envmzo1zes--create-high-quality-gifs-with-ffmpeg) *)*

3.从“wasm 文件系统”获取输出数据，并创建一个下载链接。

以下是完整的 3 个子步骤序列:

```
//Convert mp4 264 video to gif:
**async function convertVideo2Gif() {** await initWorker(); const sourceBuffer = sampleVideoData; ffmpeg.FS(
          "writeFile",
          "input.mp4",
          new Uint8Array(sourceBuffer, 0, sourceBuffer.byteLength)
        ); button.innerText = 'Processing...';
        startRunning(); ffmpeg.setProgress(({ratio}) => { button.style.setProperty('--load', ratio); if (ratio !== 0) {
                button.innerText = 'Converting...';
          } }); //Run the ffmpeg: 
 **let res = await ffmpeg.run('-i', 'input.mp4', '-vf', 'fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse', 'output.gif');** **//Retrieve the result:**        const output = ffmpeg.FS("readFile", "output.gif"); //Provide downloadable link to file:
        let videoDownloadLink = getDownloadLink(output,       "output.gif");
        if (videoDownloadLink)
          filesElement.appendChild(videoDownloadLink); videoDownloadLink.click(); stopRunning(); button.innerHTML = 'Convert';
        button.classList.add('hidden');
        button.classList.remove('gray');
        button.style.setProperty('--load', 0);
        uploadButtons.classList.remove('hidden'); imgTag.src = ''; videoTag.src = '';
        videoTag.classList.add('hidden');}
```

以下是创建可下载链接的功能:

```
//Generate downloadable link
**function getDownloadLink(fileData, fileName) {** if (fileName.match(/\.jpeg|\.gif|\.jpg|\.png/)) { var blob = new Blob([fileData]); if (navigator.share) {
            const fileToShare = new File([blob], fileName); navigator.share({
              files: fileToShare,
              title: 'Converted GIF',
              text: 'Converted GIF',
            });
          } else { var src = URL.createObjectURL(blob);
              var a = document.createElement('a');
              a.href = src;
              a.download = fileName; return a; } } else { var a = document.createElement('a');
          a.classList.add('button');
          a.download = fileName;
          var blob = new Blob([fileData]);
          var src = window.URL.createObjectURL(blob);
          a.href = src;
          a.textContent = 'Download result';
          return a;
        }
    }
```

## 第五步:添加一个别致的 CSS:

这里有一个不错的 CSS 技巧:加载程序接收*比率*变量，并呈现加载栏 CSS 动画:

```
button.style.setProperty(' — load', ratio);// use in js script
```

以下是完整的 CSS 文件:

第 6 步:添加 vercel.json

为了隔离文件，我们需要指示 Vercel(在本例中)提交 site isolated: vercel.json 内容:

# 就是这样！

这是在 Vercel 的一个独立站点上进行的演示:

![](img/cab01404a83f20c2e337d5d00ef9b71c.png)

[https://high-quality-gif.vercel.app](https://high-quality-gif.vercel.app/)

*使用 vercel.json 文件配置隔离选项。*