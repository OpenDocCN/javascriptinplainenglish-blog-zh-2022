# 净化你的 HTML 并在 React 中保持它的风格

> 原文：<https://javascript.plainenglish.io/sanitize-your-html-and-keep-its-style-in-react-1ff9fdd8e3cc?source=collection_archive---------3----------------------->

## 净化 HTML 是避免 XSS 攻击的一部分，但是如何保持你的 CSS 在里面呢？

![](img/ac173d5adb81726337935c7f734c5c5d.png)

How to make your article trendy (Photo by [cottonbro](https://www.pexels.com/@cottonbro?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/person-holding-clear-glass-bottle-4114703/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels))

净化你的 HTML 可以让你**避免 XSS 漏洞**，让你的应用**更安全**。

在 React 中，如果你打算使用`dangerouslySetInnerHTML`，你可能想要**净化你的 HTML** ，并确保它不会使你的应用程序**易受攻击**。

# 如何净化我的 HTML 代码？

因为在 React 中没有本地的方法来做这件事(不幸的是，我们将求助于一个外部库)。

我为这个操作找到的最佳选择叫做 [**dompurify**](https://github.com/cure53/DOMPurify) 。你所要做的就是安装它:

```
npm install -i dompurify
```

在您的代码中导入它

```
import dompurify from 'dompurify';
```

然后就*净化*你的 HTML！

```
dompurify.sanitize(MyHTMLString);
```

现在，在这个配置中，**样式没有被保留**,因为净化去掉了很多 HTML。为了保持您的风格，我们将使用作为函数的第二个参数给出的选项。

我们正在寻找的选项是`FORCE_BODY: true`。因此，让我们将它添加到我们的代码中:

```
dompurify.sanitize(MyHTMLString, {FORCE_BODY: true});
```

瞧啊。现在你应该保持你的风格，并且能够安全地将你的 HTML 字符串插入到`dangerouslySetInnerHTML`中！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*