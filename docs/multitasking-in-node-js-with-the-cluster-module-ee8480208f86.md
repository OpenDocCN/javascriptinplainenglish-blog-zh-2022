# Node.js 中使用集群模块的多任务处理

> 原文：<https://javascript.plainenglish.io/multitasking-in-node-js-with-the-cluster-module-ee8480208f86?source=collection_archive---------7----------------------->

## Node.js 中使用集群模块进行多任务处理的教程。

![](img/c680516394ec317d80a6f42494b7fc8b.png)

我们已经知道 Node.js 是单线程的，这意味着它将在一个可能有多个内核的系统中使用一个处理器内核。尽管对于单线程系统来说，它很好地处理了负载，但肯定还有优化的空间，集群模块就是这样做的一种方式。

引入集群模块是为了通过在多个处理器内核上运行工作进程/子进程来扩展应用程序的执行。这些进程共享同一个服务器端口，但即使使用同一个端口，它们最终也是独立的进程。所以他们每个人都有自己的 V8 实例、事件循环、自己的内存等等。这些进程使用 IPC(进程间通信)通道与父进程通信。我们将在本教程中讨论所有的特性，所以让我们开始吧。

Youtube 上也有这个教程的视频版本。

# 我们试图解决的问题

让我们通过键入`npm init -y`快速设置一个节点项目。(为了方便起见，我将添加 express，但您不必这样做)。通过键入`npm i express loadtest`安装 express 和 loadtest。在本教程的后面部分，我们将使用 loadtest 来研究使用集群模块可以获得的性能优势。安装完成后，创建一个名为 nonCluster.js 的文件，并复制这段代码(为了比较，这个文件的代码为**，没有**集群模块)。

```
const app = require("express")()
const port = 3000;app.get("/**heavy**", (req, res) => {
   let counter = 0;
   while (counter < 900000000) {
      counter++;
   } 
   res.end(`${counter} iterations completed! \n`);
})app.get("/**light**", (req, res) => {
   res.send(`Done \n`);
})app.listen(port, () => console.log("Listening to port 3000"));
```

这是一个非常简单的快速应用程序，有两个请求。`/heavy`端点执行 CPU 密集型任务，阻塞事件循环。`/light`端点立即返回响应。简单！

现在运行服务器，首先向`/heavy`发出请求，然后向`/light`端点发出请求。`/heavy`端点显然需要时间，但是您会注意到`/light`端点也需要同样多的时间。这是因为`/heavy`端点占用了计算请求的时间，因此阻塞了事件循环。因此，在`/heavy`请求之后发出的任何请求现在都必须等待其完成。

# 问题的解决方案

所以为了避免这种堵塞，让我们添加集群模块。在一个名为 **cluster.js 的新文件中，**复制了这段代码:

我们来分析一下。最初，当你有一个单一的进程，它解决所有的请求进来。现在我们使用集群模块，将有两种类型的流程。一个**父/主**和一个**子**进程。最初，当服务器启动时，它将启动一个进程集群。此后，每当有人向服务器发出请求时，父进程就会将请求转发给子进程(通常以循环方式)。然后，子进程将最终解析该请求。

```
if(cluster.isMaster){
   //spin up cluster of processes
} else{
   //resolve request
}
```

在`if`块中，我们将检查当前进程是否是父进程。集群模块有一个名为`isMaster`的属性，它让您知道当前进程是子进程还是父进程。如果是父进程，那么我们使用 fork 方法创建集群。(我们只加速与系统中存在的内核总数相等的进程，以避免调度开销。)
如果它不是父进程，那意味着它是子进程。所以这个子进程现在实际上负责解析请求。它将拥有所有的 API 端点及其相应的逻辑。

```
cluster.on("**online**", (worker) => {
   console.log("Worker " + worker.process.pid + ' is online.');    }) cluster.on('**exit**', (worker, code, signal) => {
   console.log(`${worker.process.pid} exited with code ${code});
   console.log('Starting a new worker');        
   cluster.fork();
});
```

在派生一个新的 worker 之后，它会用一个`**online**`事件来响应。我们将在父进程上监听这个事件，看看是否所有的进程都按照预期创建。

当一个工人死亡时，集群模块发出一个`**exit**`事件。因此，为了让我们的应用程序不停机，我们将在一个进程停机时派生一个新的进程。这样，即使任何其他流程由于任何有意或无意的原因而关闭，我们也将始终有一组流程在运行。

好吧，这看起来不错。现在，如果您运行这个文件，并发出相同的请求(首先向`/heavy`端点，然后向`/light`端点),您将看到它像预期的那样工作，没有阻塞事件循环。因此，添加一组进程确实有所帮助。现在让我们使用 loadtest 包来做一些相对繁重的测试。

既然您已经运行了集群应用程序，那么让我们首先测试它。键入`loadtest -n 1000 -c 100 [http://localhost:3000/heavy](http://localhost:3000/heavy)`运行测试。(如果没有全局安装 loadtest，只需在命令开头添加 npx。)

**-n** 代表请求的总数，我已经设置为 1000。
**-c**代表并发。它基本上模拟了一个真实的环境，在这个环境中，一个应用程序同时接收来自多个客户端的请求，在本例中，将有 100 个并发客户端。

这些是“**集群化”**应用程序的汇总结果。

```
**//With cluster** 
Total time : 7.178850510999999 s
Requests per second : 139
Mean latency : 685.8ms
```

现在让我们切换到"**非集群化"**应用程序，再次运行相同的测试。

```
**//Without cluster**
Total time : 27.252680297999998 s
Requests per second : 37
Mean latency : 2583.1 ms
```

使用集群时，整体性能明显有显著提高。但是有一个问题。这两个测试都是针对`/heavy`端点的，这是一个 CPU 密集型操作。让我们尝试运行相同的测试，但是这次是针对`/light`端点。

```
**//With cluster**
Total time: 0.5144123509999999 s
Requests per second: 1944
Mean latency: 48.8 ms**//Without cluster**
Total time: 0.45111675100000004 s
Requests per second: 2217
Mean latency: 42 ms
```

惊喜惊喜。在本例中使用集群时，我们实际上获得了相对较差的性能。这是为什么呢？

你看，Node.js 主要是为 I/O 操作设计的，它在很大程度上不会阻塞事件循环。因此，因为它知道如何处理这些类型的操作，所以添加额外的进程并将请求路由到这些进程中的每一个最终是一种开销，这很可能是不需要的。然而，在 CPU 密集型阻塞操作的情况下，如果在我们确实需要集群的进程之间划分请求数量，效果会更好。

所以它最终归结为你的应用程序是为什么而设计的。如果您有一个微服务架构，并且有一个处理 CPU 密集型操作的特定服务，您可以为该特定服务启动一个集群，其余的可以由您的单线程节点进程处理。

这就是在 Node.js 应用程序中处理集群的方式。它有自己的一套注意事项，在将它添加到您的代码库之前，您需要了解它们。这篇文章是我们研究 Node.js 中多任务处理的系列文章的一部分。

*   [**node . js 中多任务带子进程**](/multitasking-in-node-js-with-child-process-d82841fd8d29)

Youtube 上也有这个教程的视频版本。

如果你有任何疑问或建议，你可以在评论中提出，或者通过我的任何一个社交网站与我联系。干杯！

[YouTube](https://www.youtube.com/channel/UCaktnqx_IENyT5T2lJ3F09w)
LinkedInT5[Twitter](https://twitter.com/themangalorian)T8[GitHub](https://github.com/AkileshRao)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。****