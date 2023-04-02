# 如何使用原生 JavaScript 共享 API

> 原文：<https://javascript.plainenglish.io/how-to-use-the-native-javascript-share-api-6ec67399a9d3?source=collection_archive---------5----------------------->

## 教程

## 让用户共享他们安装的应用程序的文本、链接和文件。

![](img/0b5a890ca9b2e2e42dbf8b2f8291e191.png)

原生 Web Share API 允许用户与安装在设备上的其他应用程序共享文本、链接和文件，方式与特定于平台的应用程序相同。让我们来看看如何使用这个新功能。

## 如何使用 Web Share API 共享链接和文本？

这个 API 在 navigator 对象上公开了一个`share()`方法。这是一个基于承诺的方法，有一个必需的 properties 对象。您至少需要传递下列属性之一:

*   **标题** —例如，共享的主题被用作电子邮件的主题。
*   **text** —例如，消息的正文被用作电子邮件内容。
*   **url** —您想要分享的 url 会附加在您的正文之后。
*   **文件** —例如，您想要共享的文件被用作电子邮件的附件。

下面的代码示例显示了使用本机 share 方法并将其绑定到一个简单的按钮 click 是多么容易:

## 如何用 Web Share API 共享文件？

为了使用 Web Share API 共享文件，使用`navigator.canShare()`方法添加一个检查来测试文件是否可以共享是一个好主意。

然后你可以在`files`属性中添加文件作为数组。

## 浏览器对 Web 共享 API 的支持

![](img/82716969e4b86248e54bde646f33fc9c.png)

浏览器对 Web Share API 的支持非常好，但是 Firefox 不支持。有趣的是，尽管 Chrome 在 Windows 和 Chrome OS 上支持它，但目前它在 macOS 或 Linux 发行版上不支持它。

## 资源

*   [can use—Web 共享 API 浏览器支持表](https://caniuse.com/web-share)
*   [MDN — Navigator.share 文档](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share)

## 结论

Web Share API 是一个很棒的特性，在一些网站上可以提供一种用户友好的共享方式。这比一堆自定义的共享链接更容易实现。此外，它会根据用户安装的应用程序自动显示用户选项。

感谢阅读。如果你对此有想法，一定要留下评论！

如果你喜欢我的内容，并想支持我的努力，考虑通过[我的会员链接](https://medium.com/@WesleySmits/membership)成为一个媒体订阅者。这不会花费你任何额外的费用，但 Medium 会把部分收益给我，让我推荐你。

如果你愿意，你可以在 [LinkedIn](https://www.linkedin.com/in/wesley-robert-smits/) 或 [Twitter](https://twitter.com/iamwesleysmits) 上与我联系！

[](https://medium.com/@WesleySmits/membership) [## 通过我的推荐链接加入 Medium-Wesley Smits

### 阅读韦斯利·斯密特(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

medium.com](https://medium.com/@WesleySmits/membership) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*