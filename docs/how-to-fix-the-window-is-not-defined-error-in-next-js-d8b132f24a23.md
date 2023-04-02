# 如何修复 Next 中的“窗口未定义”错误？射流研究…

> 原文：<https://javascript.plainenglish.io/how-to-fix-the-window-is-not-defined-error-in-next-js-d8b132f24a23?source=collection_archive---------2----------------------->

![](img/a1272044fc5b573db18c1b0a43390b8e.png)

Photo by [Marten Bjork](https://unsplash.com/@martenbjork?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇简短的文章中，我将在接下来解释为什么会出现“窗口未定义错误”或“文档未定义错误”。JS 以及如何修复它。

# 为什么我会看到这个错误？

我正在为餐馆构建一个订单管理系统，并认为 Next 是最好的框架，因为我不想担心路由问题，并且仍然希望使用 React。

在我的例子中，这个错误出现了两次，原因有两个

1.  我需要向我正在构建的 API 发送一个带有有效负载的 CSRF 令牌，使用“document.cookie”触发了错误。
2.  我使用“react-apexcharts”进行数据可视化——对“window”对象进行内部调用。

起初，我认为这是我的代码中的一个错误，或者我在我的页面挂载之前过早地引用了 window 对象，并试图用 setTimeout 将它向后推几秒钟，但没有用。

基本上，我们不能访问“窗口”或“文档”对象的原因是因为 Next。JS 的服务器端渲染(SSR)功能。Next.js 在服务器上呈现我们的页面，并分块提供这些页面。

“窗口”和“文档”是客户端 API，因为 Next 在服务器端预渲染每个页面，我们不能访问这些 API，因为它们还不存在(服务器端)。

# 2.我如何修复这个错误

延迟加载和动态导入有什么特别之处吗？

> 为了防止在 **NextJS** 中的服务器端呈现，您必须使用动态导入来延迟加载您想要在客户端呈现的组件。

我在网上搜寻解决方案，在查阅了相关文档后，我发现了动态导入及其帮助。

Dynamically importing components

正如您可能已经注意到的，在第 3 行中，我将 SSR 选项设置为 false，导致它在运行时(客户端)而不是构建时(服务器端)被导入。

当试图直接访问窗口/文档对象(没有第三方包)时，有两种方法。

1.  将窗口对象存储在状态变量中以备后用(不推荐)
2.  使用客户端组件

您可以使用 useEffect 钩子来解决这个问题。查看我如何使用 useEffect 和 useState 实现了一个解决方案

Accessing window from next js

请注意，这是一个黑客，虽然它解决了这个错误，我不推荐这种方法。更好的方法是使用客户端组件。默认情况下，所有组件都是 Next.js 中的服务器组件，除非另有声明。

那么我们如何制作一个客户端组件呢？除了一个例外，客户端组件与服务器组件没有什么不同。客户端组件在所有导入之上有一个“use-client”字符串声明，告诉 Next.js 将该文件视为客户端组件，而不是服务器组件。

```
'use-client' 
// at the top of the page
// before any imports

... // imports
// you don't need to use dynamic imports in Client components

export const MyComponent = ({ props }) =>{
  return(
    <div>...</div>
  )
}

export default MyComponent;
```

既然我们已经确定了这个错误的原因并修复了它，那么在您自己的代码库中跟踪这个错误的原因应该没有问题，特别是当您使用任何引用“window”或“document”的第三方包时。

我希望这篇文章对你有所帮助。感谢您的阅读，祝您编码愉快！

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[*YouTube****，以及***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*