# 异步 JavaScript 的传奇:CSP

> 原文：<https://javascript.plainenglish.io/the-saga-of-async-javascript-csp-cb25ee18a46a?source=collection_archive---------6----------------------->

使 ES6 生成器成为异步编程发电站

![](img/3dec5a20583b269e2d0fd505031b787a.png)

# 介绍

在[之前的系列](https://medium.com/javascript-in-plain-english/the-saga-of-async-javascript-generators-40b517029b68)中，我们发现使用承诺和生成器的组合以同步方式编写我们的异步代码确实是可能的。我们的增强功能可以异步和独立运行，能够按需暂停和恢复。它们很像我们主程序中孤立的小程序！但是，当您开始编写一些真实世界的场景时，您会遇到这样一种情况，这些微小的独立部分需要相互通信并同步它们的执行。在本文中，我们将向自己介绍一种新的模式，这种模式有望让我们以一种方便且可伸缩的方式用生成器构造我们的异步代码，解决并发性给我们带来的最常见的挑战。

# 什么是 CSP

CSP 代表**通信顺序进程**，是在我们的应用程序中建模并发性的另一种方式。CSP 是将你的程序分解成一组独立的、自包含的黑盒**过程**，这些过程响应各种事件并自己产生事件。为了允许这些流程进行通信，我们使用了**通道**——一个中间人实体，它的作用就像一个管道，在流程之间分发事件。与渠道的交互方式构成了大部分模式。CSP 背后有一个强大的数学理论，它定义了一组定律和抽象来使它工作，但谢天谢地，我们不必是数学博士才能开始使用它。

# 概述

在现实世界中，事物之间相互交流并对事件做出反应。我们甚至倾向于根据事物对事件的反应来思考许多事情。我们如何才能采取正确的心态来看待现实世界的对象作为一个过程？我们可以试着把某样东西想象成它对事件的一系列**反应。让我们想象一台咖啡机。当你打开它时，它会加热水。当你点击“拿铁”的时候，它就做了一杯拿铁。我们呢？当我们想要一杯咖啡时，我们去咖啡机旁煮咖啡。当咖啡准备好了，我们就喝它。你和咖啡机只是两个通过接口相互通信的进程。它是同步你的动作的界面，并且让你知道咖啡机什么时候完成加热并且准备好让你选择一杯咖啡。否则，在不知道机制如何运作的情况下，你的行动将会混乱无序，导致咖啡机坏掉，薪水也不丰厚。在这个特殊的例子中，一个接口就像一个**事件通道**，为我们机器和人内部的实际咖啡制作机制服务。我们当然不需要知道是什么让我们成为幕后的咖啡，只要我们知道如何应对它传达给我们的事件。**

# 什么是渠道

您可以将通道视为一组不断更新的数据或事件。在某种意义上，它也可能类似于队列。总之，通道代表了代码之间的异步通信。你可以**从频道里拿走**它，你可以**把**东西放到频道里。通道可以有缓冲或无缓冲，缓冲器可以是不同的类型。例如，丢弃缓冲区，当满时，将丢弃所有传入的值。滑动缓冲区将接受传入的值，并丢弃缓冲区中最旧的元素。你为什么需要缓冲器？想象你是一个酒保，点了一杯莫吉托。一旦你喝完了莫吉托，你就按铃，希望你点的菜能被接受。在处理其他订单之前，你会坐下来等别人来拿吗？当然不是，你可以在吧台上放 10 杯莫吉托，所以你的“缓冲”容量是 10 杯。

# 保护命令

如上所述，CSP 在通信和渠道方面实施了一套规则。其中最重要的一个是**背压**的概念。想象两个人分别站在水管的两边，每个人都有一个水龙头。我们不能把水推给对面的人**，直到他打开水龙头**并允许我们送水。我们需要等待。大多数 CSP 实现中的保护命令具有相同的概念。在完成我们的 **put** 操作之前，我们必须等待有人准备好从通道中取出事件。发送方进程此时基本上被阻塞了。当一个进程想要接收一个事件时，它也会被阻塞，直到事件到达通道。保护命令就像一种同步机制，让两个基本独立的进程在特定事件上同步。

# 给我举个例子

在学习模式时，我试图创建一个 CSP 的基本实现。除了对模式有更深的理解之外，另一个重要的好处是我可以向您展示这个库的例子。该代码演示了我前面提到的一个超级简单的咖啡机示例:

```
import { makeChannel } from 'csp-coffee/channel';
import { take, put } from 'csp-coffee/operators';
import { go } from 'csp-coffee/go';
import { delay } from 'csp-coffee/utils'
​
const coffeeMachineInterface = makeChannel<string>();
​
function* person () {
    yield put(coffeeMachineInterface, 'latte');
    console.log('i want my coffee so much');
    yield take(coffeeMachineInterface);
    console.log('yummy');
}
​
function* coffeeMaker() {
    const coffeeToMake: string = yield take(coffeeMachineInterface);
    yield delay(1000);
    yield put(coffeeMachineInterface, `have a coffee ${coffeeToMake}`);
}
​
const { cancellablePromise: personPromise } = go(person);
const { cancellablePromise: coffeeMakerPromise } = go(coffeeMaker);
​
Promise.all([personPromise, coffeeMakerPromise]).then(() => {
    console.log('done');
})
```

请注意，我们将参与者表示为生成器函数，这些函数稍后会传递给一个特殊的`go`函数。这就是把我们的生成器变成**进程**的原因。它只负责承诺、库操作符( **put** 、 **take** )以及它们执行的正确顺序。它还返回一个 promise，当生成器函数执行完毕时，这个 promise 将被解析，如果我们试图将这个库合并到大量使用 promise 的代码中，这将非常方便。

# 它如何让事情变得更好？

它不是，它只是组织异步代码的一种不同方式。当然，在每一种情况下，你都不需要这样的抽象。但是在开发几乎任何大型应用程序的某个时候，您必须处理越来越多的并发问题。当试图使用承诺、RxJS 或简单的回调来解决这些问题时，您开始将业务代码放入事件处理程序中。随着此类代码数量的增加，推理业务逻辑变得越来越困难，因为您必须将遍布应用程序的回调组合成一个难题。CSP 通过在中间引入通道来解决这个问题，它将通信和流量控制分开。它吸收了生成器的所有优点——看起来同步的代码、暂停等——并通过为通信提供一个抽象和一组清晰的规则，使它更上一层楼。

# 结尾部分

这篇文章似乎比我之前预期的要短得多。对于一篇文章来说，CSP 可能为您提供的方法和函数的数量太多了。重要的是，你不需要知道他们所有人来理解这个概念。我们从上一篇关于生成器的文章中学到了一些东西，并看到了它是如何发展成为一个更加重要的工具的。我将在下面留下几个链接，供您探索 API 并更好地理解一个实现可能具备的能力。

# 资源

[我尝试将部分核心异步移植到 JavaScript](https://github.com/RomanSarder/csp-coffee)

[Clojure 核心异步库](https://github.com/clojure/core.async)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*