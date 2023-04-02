# JavaScript Runtime Node.js 19 保持 HTTP 连接活动并替换 Nodemon！

> 原文：<https://javascript.plainenglish.io/javascript-runtime-node-js-19-keeps-the-http-connection-alive-and-replaces-nodemon-6925ce113271?source=collection_archive---------5----------------------->

## 很酷的新功能，少了一个要安装的 npm 包💪🏾

![](img/112ac0dbc002b9581e7ef24898ca4bce.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/news?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

上周，Node.js 社区发布了 Node.js 19，这是第 18 版发布 6 个月后的结果。最新版本的开源 JavaScript 运行时环境中包含了一个新的实验性特性，可以在重要文件更新时重新启动这个过程。此外，HTTP 的保持活动功能会立即打开。

内部已经做了一些改变:JavaScript 引擎 V8 的 10.7 版本和处理 HTTP 处理的 8.1.0 版本的`llhttp library`，现在在运行时环境中使用。

四月份发布的 Node.js 18 将在接下来的一周进入长期支持(LTS)。运行总共三年，运行时的偶数版本号随着奇数版本号的发布而过渡到 LTS 阶段，而奇数版本号随着随后偶数版本号的发布而达到其寿命终点(EOL)。因此，Node.js 18 将支持到 2025 年 4 月 30 日，而 Node.js 19 将只支持到 2023 年 6 月 1 日。

# 保持连接

这个新版本(Node.js 19)默认启用`keepAlive`。传出 HTTP(S)连接受 HTTP/1.1 中包含的保持活动功能的约束，该功能重用当前连接，通常会提高性能。超时默认设置为 5 秒。

启用`keepAlive`会带来更好的性能，因为默认情况下会重用连接。

此外，代理现在可以解释服务器可能发送的任何响应`keepAlive`消息。客户端通过这个头被告知保持连接的时间。另一方面，当使用`close()`方法时，Node.js HTTP 服务器现在将立即断开不活动的客户机(这些客户机利用 HTTP Keep-Alive 来重用连接)。此外，Node.js HTTP(S)/1.1 请求的吞吐量/性能可能会有默认的提高。

# 加密现在是稳定的！

Node.js 19 稳定了 WebCrypto API，可以由`globalThis.crypto`或`require('node:crypto').webcrypto`使用(使用以下算法的情况除外:X448、X25519、Ed448 和 Ed25519)

# 可用的观察模式

严格来说，仍然标记为实验性的(几乎)新命令行参数`--watch`，已经做成了 18 系列的运行时环境，从 18.11 版本就已经知道了。如果它是活动的，运行时检查文件的更改，如果是，重新启动进程。当文件由以下人员运行时，它可以被激活:

# 结束语

快速更新新 Node.js 版本中的重要新变化。由于最新的 LTS 版本 16 将于明年弃用，您应该考虑更新到 18 LTS 或 19。这一过程可能会对你的应用程序造成严重损害，你应该尽早。

我的建议:**现在就开始！**

此外，除了创新之外，值得注意的是 Node.js 19 不再为分析工具 DTrace、SystemTap 和 ETW(Windows 事件跟踪)提供连接。使与工具的交互保持最新显然太复杂了。

```
**Want to Connect?**Feel free to connect with me on [my blog](https://www.knulst.de/), [LinkedIn](https://www.linkedin.com/in/paulknulst/), and [Twitter](https://twitter.com/paulknulst).
```

*本文最初发表于我的博客*[*https://www . paulsblog . dev/JavaScript-runtime-node-js-19-keeps-the-http-connection-alive/*](https://www.paulsblog.dev/javascript-runtime-node-js-19-keeps-the-http-connection-alive/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***