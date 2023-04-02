# 使用 Node.js 的服务器发送的事件

> 原文：<https://javascript.plainenglish.io/server-sent-events-with-nodejs-bbdc9a9584cb?source=collection_archive---------1----------------------->

## 从您的后端接收定期更新，而不发送垃圾 HTTP 请求

![](img/75c3c5b9ac688bf66fcb38be06980f73.png)

Unrelated, I just liked the image (Photo by panumas nikhomkhai: [https://www.pexels.com/photo/close-up-photo-of-mining-rig-1148820/](https://www.pexels.com/photo/close-up-photo-of-mining-rig-1148820/))

在我的一份工作中，我们正在处理一个案例，前端必须每分钟检查是否有新的通知。我们还使用了 HTTP2，所以 WebSocket 并不是一个真正的选择。然而，我听说过一个叫做服务器发送事件(或 SSE)的 JavaScript 特性。我建议，但由于“复杂性”(或懒惰，不确定)，领导决定去用 HTTP 请求垃圾邮件后端…

这就是我今天写这篇文章的原因，向您展示这是多么简单，SSE 应该比实际使用的更多！

# 什么是 SSE

SSE 是一个服务器推送的事件系统，与 WebSockets 不同，它是单向的。一旦客户端请求与后端连接，就会打开一个通道，后端就可以发送我们想要的任意多的事件。

![](img/924999173bb7cc96490cc3c7b3978bfe.png)

Browser compatibility

SSE 兼容所有现代浏览器(如果 2022 年你还在支持 IE11，那就是你的问题了！)哪个用起来都是好加分！

## 它是如何工作的

SSE 非常简单。客户端(浏览器)将使用 HTTP2 请求与后端建立新的连接。一旦接受，通道将打开，后端将能够发送请求。通道将一直打开，直到前端决定关闭连接，这意味着如果后端关闭连接，前端将立即请求新的通道，因为它会将其视为错误。

# 我们试试吧！

## 服务器

我们将从服务器开始。在 nodeJS 中 SSE 是现成可用的，但是为了使事情更容易，我们将使用 express 来代替。

安装时使用:

```
npm install -S express cors
```

现在，让我们编写一个小型 express 服务器:

```
const express = require("express");
const cors = require("cors");const app = express();
app.use(cors());const headers = {
  "Content-Type": "text/event-stream",
  Connection: "keep-alive",
  "Cache-Control": "no-cache",
};let counter = 0;
let interval;app.get("/event", (req, res) => {
  res.writeHead(200, headers);interval = setInterval(() => {
    const data = `${JSON.stringify({ counter })}\n\n`;
    res.write(data);
    counter++;
  }, 1000);
  req.on('close', () => {
    clearInterval(interval);
  });
});app.listen(4000, () => {
  console.log("listening...");
});
```

让我们快速浏览一下这个文件。

Headers 只是定义了服务器发送给客户端的头。(别忘了我们使用的是 HTTP2，SSE 基本上是发送一种不同的响应)

然后，我们使用`writeHead`将头部发送回客户端并打开流。

然后，在`setInterval`中，我们每秒向客户端发送一个新版本的计数器。

注意，响应需要是一个字符串，我们需要两个`*\n*`在末尾，否则浏览器永远不会接受数据。

使用`req.on('close')`，我们监听客户端关闭连接(记住，客户端拥有控制权！)

最后，我们使用了`cors`模块，因为我们的客户端和服务器不在同一个地方，否则我们会有严重的错误！

## 前端

对于前端，我们将使用一个基本的 HTML/JavaScript 页面，因为我们不需要使用任何大的框架，并且 SSE 是框架不可知的:

```
<html>
  <body>
    <button id="connect-btn">Connect</button>
    <button id="stop-btn">Stop</button>
    <script>
      const onMessage = (event) => {
        const data = JSON.parse(event.data);
        console.log(data);
      };let eventSource;const connectBtn = document.getElementById("connect-btn");
      const stopBtn = document.getElementById("stop-btn");
      connectBtn.addEventListener("click", () => {
        eventSource = new EventSource("[http://localhost:4000/event](http://localhost:4000/event)");
        eventSource.onopen = () => {
          console.log("opened");
        };
        eventSource.onmessage = onMessage;
      });
      stopBtn.addEventListener("click", () => {
        eventSource.close();
      });
    </script>
  </body>
</html>
```

让我们不要太关注 HTML，有趣的是我们的 JavaScript 代码。

当点击 connect 按钮时，我们正在实例化一个新的`EventSource`，它将连接到我们的后端。然后我们分配两个监听器。

第一个在连接打开
( `eventSource.onopen`)时触发，将触发一次(连接时)

第二个是为每条消息触发的(`onmessage`)。我们将接收一个事件作为参数(参见 JS 标签顶部的`onMessage`箭头功能)

最后，当单击 stop 按钮时，我们只需关闭 eventSource！

就这么简单！SSE 使用起来非常简单，允许您打开一个通道，而不必使用 WebSockets(或者向后端发送新数据)

我希望你喜欢这篇文章，如果你喜欢，不要犹豫鼓掌或关注！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*