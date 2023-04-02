# 前端工程师如何压缩图片，你可以这样做

> 原文：<https://javascript.plainenglish.io/how-front-end-engineers-compress-pictures-you-can-do-this-80988ea447d8?source=collection_archive---------8----------------------->

![](img/e2109d69c8658458525e9db676cf67cd.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们从 PS 等工具导出的图片，或者美术直接给的剪切图，都是未压缩的，比较大。在这里，有优化的空间。

# 1.TinyPng

TinyPNG 使用智能的“有损压缩技术”来减小 WEBP、JPEG 和 PNG 文件的文件大小。通过选择性地减少图像中的“颜色数量”,使用更少的字节来存储数据。这种影响几乎看不见，但会对文件大小产生非常大的影响。

用过 TinyPng 的人都知道，它的压缩效果非常好，体积大大减小，显示效果也差不多。所以选择它作为压缩工具是个不错的选择。

TinyPng 提供了两种压缩方法:

*   通过在官网手动压缩
*   压缩通过官方测试

作为一个程序员，我不能接受手工一个一个上传压缩文件的方法。所以选择第二种方法，通过封装一个工具自动压缩项目中的图片，彻底解放双手。

# 2.工具类型

第一步，思考这个工具的“目的”是什么？没错，“压缩图片”。

第二步，思考压缩哪个“环节”？没错，“上映前”。

从这个角度来说，开发一个 webpack 插件是一个不错的选择。打包“生产环境”代码时，启用插件来处理图像。然而，这将面临两个问题:

*   页面迭代，加了几张图。重新打包上线时，旧图片会被多次压缩。
*   无法选择哪些图像要压缩，哪些不要压缩。

虽然以上问题可以通过“配置”来解决，但是每个包都需要一个特殊的配置，有点麻烦。看来外挂不是最好的选择。

使用“命令行工具”可以完美解决以上两个问题。在打包“生产环境”代码之前，执行“压缩命令”，通过命令行交互选择要压缩的图像。

# 3.使用

```
$ npm i yx-tiny -D
$ npx tiny
```

压缩结果为:2.64MB ==> 1.02MB

# 4.实施理念

总的来说，有五个过程:

*   **查找**:查找所有图像资源
*   **分配**:将任务平均分配给各个流程
*   **上传**:上传原图到 TinyPng
*   **下载**:从 TinyPng 下载压缩图片
*   **写**:用下载的镜像覆盖本地镜像

## 4.1 查找

查找所有图像资产。

通过命令行交互后，获取目标文件夹的路径，然后获取路径下的所有内容，再遍历所有内容。首先确定内容的文件信息:如果是“文件夹”，那么以文件夹路径为路径，递归调用 deepFindImg，如果不是“文件夹”，确定内容是图片，读取图片数据，推送图片。最后，返回所有找到的图像。

## 4.2 分配

将任务平均分配给每个流程。

使用 cluster 根据“CPU 核心数”创建相同数量的进程。Works 用于保存创建的流程。该列表存储要处理的压缩任务。通过遍历列表，任务被依次分配给每个进程。然后遍历作品，通过 send 方法发送流程任务。通过监听 message 事件，使用 pageNum 记录流程任务的完成情况，当所有流程任务执行完毕后，流程关闭。

## 4.3 上传

官方的 tinify 工具有“500 张/月”的限制。超过限额后，需要付费。

![](img/313518436afca24414757d56d3487432.png)

使用节点附带的 HTTPS 模块来构造请求头，并上传由 deepFindImg 返回的图像。上传成功后，会返回压缩图片的 URL 链接。

## 4.4 下载

从 TinyPng 下载压缩图像。

使用节点附带的 HTTPS 模块下载上传中返回的图像链接。下载成功后，返回图片的缓冲数据。

## 4.5 写

用本地图片覆盖下载的图片。

Process.on 监控每个进程发送的任务。当任务类型为“图片”时，使用压缩方法处理图片。当任务类型为“svga”时，使用 compressSvga 方法处理 Svga。最后，将处理后的资源写到本地覆盖旧的资源。

**压缩**

CompressImg 返回一个异步函数，先调用 upload 上传图片，再调用 download 下载，最后返回图片的缓冲区数据。

**CompressSvga**

compressSvga 的“输入”和“输出”与 compressImg 一致，目的是用 promise.all 同时调用。在 compressSvga 内部，将 Svga 解析成数据，获取 svga 的图像列表图像，然后调用 compressImg 对图像进行压缩，用压缩后的图像覆盖 data.images，最后对数据进行编码，写入本地覆盖原来的 svga。

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----80988ea447d8--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----80988ea447d8--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----80988ea447d8--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----80988ea447d8--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----80988ea447d8--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----80988ea447d8--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*