# 关于网页可访问性你应该知道的一切

> 原文：<https://javascript.plainenglish.io/everything-you-should-know-about-web-accessibility-2d743268506c?source=collection_archive---------19----------------------->

## 深入了解网页可访问性，并学习如何让我们的**网站**更易于**访问**。

![](img/a49ecec405aca424828012bb4c1f0833.png)

Photo by [KOBU Agency](https://unsplash.com/es/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇博客中，我们将讨论**网页可访问性**，从最基本的到深入理解。此外，我们还将看看如何让我们的**网站**更容易访问**。所以让我们开始吧！**

# **什么是可访问性？**

**可访问性意味着让尽可能多的人可以使用你的网站。我们倾向于认为这一切都是为了让网站对残疾人可用，但这部分是正确的。可访问性实践也有利于其他用户群体，如使用移动设备的用户或网络连接速度慢的用户。**

# **使网站无障碍的好处**

*   **为了使网站具有可访问性，我们使用语义 HTML，这提高了网站的搜索引擎优化，使您的网站更容易被找到。**
*   **提高可访问性的其他良好实践也使您的网站更容易被其他群体使用，如移动电话用户或网速较低的用户。**
*   **这也是一些地方的法律，所以你最好遵守当地的法律**

**因为可访问性主要是指让网站对残疾人来说更有用、更友好。因此，让我们了解不同类型的残疾，看看我们如何实施一些可行的步骤，使网站更容易访问。**

# **一些常见的残疾:**

*   ****有视觉障碍的人:**他们使用屏幕阅读器工具。因此，重点应该放在以这样一种方式开发一个网站，屏幕阅读器可以很容易地阅读网站的内容。**
*   ****有听力障碍的人:**视频应配有字幕，音频内容应提供抄本。**
*   ****行动不便的人:**有些人可能很难做出准确的手部动作。因此使用鼠标会很困难。所以应该使用键盘来提供控件。**

# **提高可访问性的一些可行步骤:**

**![](img/72fd7a279b49f9d5b375b03e9fbe0a07.png)**

**Photo by [Jakob Owens](https://unsplash.com/es/@jakobowens1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

1.  ****包含<标题> :** 确保在 HTML 文档中包含一个<标题></标题>标签，因为它可以提供快速参考。它很容易识别内容。**
2.  ****标题和标签:**在页面上添加清晰的描述性标题。因此用户可以很容易地获得特定部分的上下文。描述性标签帮助用户识别内容中的特定组件。**
3.  ****节标题:**节**节**节标题定义了页面内容的整体组织。标题的例子包括节、内容的子节等等。与其他识别页面内容部分的方法相比，标题是更明显的导航工具。).**
4.  ****绕过内容块的能力:**为用户提供一种跳过网页重复内容的方式。**

# ****HTML 和可访问性****

**![](img/4a0ac3110b56acbdbc33ec8db998e8f7.png)**

**Photo by [Jackson So](https://unsplash.com/es/@jacksonsophat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

****HTML** 在让一个**网站**更加**易访问**方面起着至关重要的作用。应定期遵循以下几点，以使您的网站易于访问:**

1.  ****使用语义标记:**而不是将所有东西都包装在一个< div >标签中。你应该使用浏览器友好的语义标签，如<导航>、<页脚>和<部分>等。像屏幕阅读器这样的工具可以很容易地识别网页的内容。**
2.  ****UI 控件:**最常见的 UI 控件，如按钮、链接、表单控件等，可以使用键盘进行导航。**

# **WAI-ARIA(网络无障碍倡议——无障碍丰富互联网应用)**

**![](img/b5f49d26abbaaaaa4083cc01d13e122c.png)**

**Photo by [Taras Shypka](https://unsplash.com/@bugsster?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

**WAI-ARIA 是 W3C 编写的一套指导方针，旨在改善缺乏可访问性的地方。这些指南分为三个规范:**

1.  ****角色—** 角色定义元素的类型或其用途。像导航标签一样，我们有一个导航角色(<nav role = " navigation "></nav>)。这样的角色有很多，像 role="banner "，role="search "，role="tablist "，role="tab "等等。**
2.  ****属性—** 它定义了元素的属性，给出了元素的额外信息。例如，aria-required="true "指定需要填写表单输入才能有效。**
3.  ****States —** 给出一个元素的当前状态。例如 aria-disabled="true "，它向屏幕阅读器指定该元素当前被禁用。**

# **测试和改善网页可访问性的工具**

**![](img/5203852f3e6bd309f2bb760c7c0df034.png)**

**Photo by [Dan-Cristian Pădureț](https://unsplash.com/@dancristianpaduret?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

**[**AXE dev 工具**](https://www.deque.com/axe/devtools/chrome-browser-extension/) **:** 它是一款 chrome 浏览器扩展工具，帮助你测试你的网站的可访问性。不仅如此，它还会给你一个反馈列表，告诉你哪里不足，如何进一步改进。**

**[**Google 的 Light House**](https://developers.google.com/web/tools/lighthouse)**:**它是 Google 的又一个令人惊叹的 chrome 扩展，不仅能给你无障碍测试报告，还能给你网站的性能反馈。**

# **结论:**

**谢谢你一直读到最后。希望你对可访问性有一个清晰的概念，并且你已经准备好一些可操作的步骤来使你的网站更易访问。**

**如果你想要更多这样的内容，请在媒体上关注我，订阅我的 YouTube 频道。**

**有疑问吗？通过[推特](https://twitter.com/izrajesh)联系我。**

***更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***