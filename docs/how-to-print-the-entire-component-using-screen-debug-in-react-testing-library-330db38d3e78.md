# 如何在 React 测试库中使用 screen.debug()打印整个组件

> 原文：<https://javascript.plainenglish.io/how-to-print-the-entire-component-using-screen-debug-in-react-testing-library-330db38d3e78?source=collection_archive---------6----------------------->

![](img/727d7b39f4e2dc70ac8a5b56bf4f60b3.png)

Photo by [Julia Koblitz](https://unsplash.com/@jkoblitz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我喜欢 React 测试库，如果你在这里，你可能也会喜欢它。

但是当我们用许多行 JSX 测试一个组件并试图打印它时，React 测试库不会显示整个组件。

## **问题**

> //问题🔴
> 
> screen.debug()

## **解** ✅

幸运的是，这个问题的解决方案很简单，下面的命令将在控制台中打印整个组件。

```
screen.debug(undefined, Infinity)
```

[来源](https://github.com/testing-library/react-testing-library/issues/503#issuecomment-853783968)

嗨，[在这里](https://davidjsmoreno.dev/)我们谈论软件开发、JavaScript、自学教育和其他东西。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***