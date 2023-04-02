# 如何保护你的应用免受恶意依赖

> 原文：<https://javascript.plainenglish.io/how-to-protect-your-app-from-malicious-dependencies-da640f8c8143?source=collection_archive---------20----------------------->

![](img/9e2c9f1a7f85acd0bef83327e35f7f3b.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

早在一月份，两个流行的开源库(faker.js 和 colors.js)的维护者发布了这两个库的新版本，删除了所有功能，并包含了一些记录消息的代码，这些消息将在导入模块时显示。

本文并不关注这一事件的哲学层面，而是关注由此引发的安全问题。

[](https://www.bleepingcomputer.com/news/security/dev-corrupts-npm-libs-colors-and-faker-breaking-thousands-of-apps/) [## 开发腐败 NPM 图书馆的“颜色”和“骗子”打破数以千计的应用程序

### 流行的开源库“colors”和“faker”的用户在看到他们的应用程序后感到震惊，使用…

www.bleepingcomputer.com](https://www.bleepingcomputer.com/news/security/dev-corrupts-npm-libs-colors-and-faker-breaking-thousands-of-apps/) 

这以一种非常清晰有力的方式表明，依赖关系容易受到恶意更改的攻击。这总是正确的，但是当这样的事件发生时，它提出了许多关于当前工作流安全性的问题。这是一个相当温和的情况，这可能会更糟。想象一下，一个维护者，或者一个可以访问维护者账户的黑客决定发布一个新版本，用恶意软件替换这个库。如果您的项目工作流不安全，您可能会将恶意软件下载到您的开发甚至生产机器上。

# **我们当前的工作流程**

![](img/3930ecffc8af766740bafef672b8eaa1.png)

Photo by [Axel Vazquez](https://unsplash.com/@creativeaxe?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文主要讨论 NPM 和 JavaScript 项目。但是可以从任何依赖程度高的栈的角度来研究这些概念。

我们的大多数项目使用 NPM 作为我们下载依赖项的包存储库。我们的依赖通常来自受信任和受欢迎的项目，但也可能来自任何人。这些依赖项可能有它们自己的依赖项，这些依赖项也可能有它们自己的依赖项，等等。

您是否检查了上次安装和新安装之间有什么变化？当审查对项目的依赖拉取请求时，是否验证库更新？大多数人不会。虽然这在大多数情况下没什么大不了的，但是如果依赖关系受到损害，您的开发甚至生产环境可能会很脆弱。

# **缓解问题**

![](img/005ad7868baa7ea514af67f244882a30.png)

Photo by [Collin Armstrong](https://unsplash.com/@brazofuerte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

那么，我们如何减轻这种安全风险呢？考虑到这种情况并不常见，这并不一定是一个高风险的问题，但是它很容易执行。您所需要的只是访问一个流行依赖项的发布权限。如果您只是发布一个补丁更新，它不会被大多数配置停止，因为补丁更新被视为“不间断更改”，通常包含错误修复或性能改进。

缓解这个问题的第一个方法是利用像`package-lock.json`这样的东西。这个文件包含了你的依赖树和每个包的锁定版本。这与在生产环境中运行全新安装的`npm ci`命令(带有锁定的依赖关系树)一起，有助于保持生产环境的一致性和安全性。

[](https://docs.npmjs.com/cli/v7/configuring-npm/package-lock-json) [## package-lock.json | npm 文档

### 对于 npm 修改 node_modules 树或……的任何操作，都会自动生成 package-lock.json

docs.npmjs.com](https://docs.npmjs.com/cli/v7/configuring-npm/package-lock-json) 

除了在安装/更新依赖项时检查新版本之外，您对本地部署没有太多可做的。这不仅会揭示任何新的特性或突破性的变化，还会确保项目没有受到损害。如果你不需要更新任何包，你也可以运行一个`npm ci`安装，但是如果你是维护者，这并不意味着你不能停止检查更新。请记住，修补程序更新可能包含漏洞修补程序，因此请确保经常审核您的依赖关系。

# **最坏的情况**

![](img/06e3c12d2ff6e79933e7fa03601addfe.png)

Photo by [Tanya Grypachevskaya](https://unsplash.com/@stilltane4ka?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

还有最后一件事可能会危及您对依赖项的使用，那就是对 NPM 的攻击。虽然这是极不可能的，如果 NPM 被入侵，你可能在技术上下载你认为是已知的好版本，但实际上收到的是恶意软件。这不太可能，而且是最糟糕的情况，但是最好了解攻击面是什么，以及哪里容易受到攻击。

# **结论**

虽然这些事件非常罕见，而且最近的例子也很温和，但是对于所有使用某种集中依赖库的项目来说，这些都是真正的威胁。即使安装依赖项的时间稍微长一点，在下载之前或之后，但在运行之前检查一下软件包也是值得的。虽然我希望这些事件不再发生，但我们至少要做好准备，保持警惕。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***