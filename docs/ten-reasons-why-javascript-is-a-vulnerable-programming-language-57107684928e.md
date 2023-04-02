# JavaScript 是易受攻击的编程语言的 10 个原因

> 原文：<https://javascript.plainenglish.io/ten-reasons-why-javascript-is-a-vulnerable-programming-language-57107684928e?source=collection_archive---------10----------------------->

![](img/445a447e69200519940bf548f9ac84c8.png)

Photo by [Hello I’m Nik](https://unsplash.com/@helloimnik?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/sad?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript 是当今最流行的编程语言之一，这意味着有大量的开发人员正在学习和使用它。然而，JavaScript 有一些漏洞，即使是经验丰富的程序员和在其网站上使用这种语言的公司也会感到惊讶。以下是 JavaScript 是一种易受攻击的编程语言的 10 个原因。

# 第一:JavaScript 安全缺陷

攻击者可以操纵网页中嵌入的 JavaScript 来运行恶意代码。这使得他们能够利用使用未打补丁的浏览器(如 **Internet Explorer 6、7 和 8** )的计算机上的内存和其他漏洞。

浏览器供应商如**谷歌**已经为这些安全漏洞开发了他们自己的补丁，但是在让用户升级他们的浏览器时遇到了麻烦。随着近 **9 亿用户**仍在使用旧版的 Internet Explorer，在没有浏览器供应商任何干预的情况下，网络罪犯有很大的空间利用不安全的浏览器。

# 第二:跨站点脚本(XSS)问题

与任何其他编程语言一样，JavaScript 的安全性也很重要。它最大的威胁之一是**跨站脚本(XSS)** 。当有恶意代码从合法网站窃取信息，甚至向其中注入另一段代码时，就会发生这种情况。JavaScript 安全性的另一个问题是弱密码；因为**网站通常不会强迫你使用复杂的密码，**XSS 攻击者可以通过找出你使用的密码，轻松窃取你所有的凭证和其他有价值的数据。

# 第三:远程代码执行

JavaScript 代码可以很容易地通过网络连接从一台计算机发送到另一台计算机，这使得它非常容易受到攻击。这就是为什么开发人员必须使用诸如 **C#** 和 **Java** 等编程语言提供的安全特性，以确保他们编写的是安全的代码。如果他们做不到这一点，他们的应用程序的用户就会受到严重的安全威胁，比如被监视或者他们的机器被接管。

因为 JavaScript 没有任何针对恶意黑客的内置代码，所以任何攻击都变得容易十倍，因为您不需要编写数千行复杂的代码，这些代码会导致开发人员高度疲劳并在调试过程中浪费时间。

# 第四:缺乏数据加密

因为 JavaScript 通常托管在 web 服务器上，所以任何访问者都可以从任何地方访问它。这意味着如果有人入侵你的网站或服务器，他们可以直接从你的 JavaScript 代码中提取你的所有数据。

相比之下，像 C 和 Java 这样的编程语言有适当的框架来确保只有授权用户才能访问他们的数据或读取源代码——这样即使有人得到了它们，他们也只能看到你想让他们看到的东西(*尽管黑客仍然有办法绕过防火墙*)。虽然对 JavaScript 也应该采取一些预防措施(T2，比如加密)，但是大多数程序员不包括这些，因为浏览器缺乏对这些特性的本地支持。

# 第五:缺乏传输层保护

web 应用程序(*和大多数其他客户端-服务器系统*)的通信模型是无状态的，这意味着每个 **HTTP** 连接都独立于之前的连接。这个模型意味着会话数据不能从一个页面请求传递到另一个页面请求，**迫使开发人员使用 cookie**或其他传输层来保存信息。

因为 cookies 很容易被恶意行为者拦截和修改，所以它们被认为是不安全的，并且作为一种传输保护形式经常被忽略。最重要的是，**跨站点脚本漏洞在许多情况下允许攻击者读取 cookie 内容。**因此，虽然我们并不总是可以选择使用 **SSL/TLS** ( *即，当网站运行在 HTTP* 之上时)，但这是您应该尽可能考虑做的事情。

# 第六:浏览器操作

JavaScript 不仅仅用于客户端脚本。它也广泛用于服务器端和设备编程。说到浏览器操控， **JavaScript 只受限于你的想象力**。操纵浏览器可以让你访问安全摄像头、电话、麦克风、谷歌搜索等等。如果你能想象得到，很有可能有某种方法可以通过 JavaScript 来实现。如果没有 JavaScript 及其客户端脚本语言——**html 5**，互联网就不会有今天！

# 第七:糟糕的认证实践

如果你以一个匿名用户的身份来看待你所有的 JavaScript 代码，那么你就不需要努力去做好它。你可以做你想做的事，没人会注意到。不幸的是，对于知道在哪里(何时)查找的用户来说， **JavaScript 很容易被黑掉**，因为黑客有太多的方法可以利用糟糕的认证实践，用别人的凭证逃跑。

黑客喜欢窃取密码，因为这样可以很容易地快速侵入账户，窃取或出售信用卡信息、个人信息、在线活动历史或敏感文档。如果你关心保护你的站点免受潜在的攻击，那么不要使用 JavaScript 不值得冒这个险。

# 第八:软件在上市前没有经过严格的测试

我们都曾在自己喜爱的软件中遇到过错误和故障。这些很烦人，但它们很少对我们的个人数据和隐私构成威胁。不幸的是，**其他软件**并不总是如此——包括像 JavaScript 这样的开源程序。

虽然大多数此类程序都经过了严格的测试，但其他程序直到向公众发布后才通过有效的测试机制。到那时，你可能已经很容易受到那些等待时机的人的攻击。

# 第 9 名:未知的未知 JavaScript 的阴暗面

JavaScript 是一种非常流行的编程语言，这是有充分理由的。尽管有这么多不同的浏览器，但是当你用 JavaScript 编写一些东西却不能工作时会发生什么呢？当你的代码能在 **Chrome** 上完美运行，但不能在**ie 浏览器**或 **Safari** 上运行时，会发生什么？答案是你需要了解这些浏览器之间的区别。

很容易认为，由于 JavaScript 非常流行，它已经足够标准化，在一种浏览器中编写的任何 JavaScript 代码都可以在另一种浏览器中运行。然而，这不是真的。为了确保你的网站在所有主流浏览器上看起来都很棒( **Chrome，Firefox，Safari，IE** )，确保你用所有可能的浏览器测试你的网站。如果有人用 Opera 访问你的站点，而它看起来很奇怪——太糟糕了！

# 第十:脆弱的文档

这与其说是使用 JavaScript 的问题，不如说是使用任何解释型编程语言的问题。JavaScript 最大的特点之一是它的代码 c **可以在不同的环境中执行，而无需修改。**例如，如果一个程序需要在多个操作系统上运行，JavaScript 可以节省时间和精力，因为它不必一遍又一遍地重写某些代码段。

但是因为有许多不同的方法来实现 JavaScript 代码，所以在开发的每个阶段都要有文档记录(T12 和良好的文档记录)是很重要的，这样一切才能从头到尾顺利进行。如果你不这样做，那么**你可能会损失无数的时间来重写整个程序或调试问题**，这些问题本可以通过更好的初始文档来避免。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*