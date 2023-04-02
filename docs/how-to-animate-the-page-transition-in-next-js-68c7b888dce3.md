# 如何在 Next.js 中制作页面过渡动画

> 原文：<https://javascript.plainenglish.io/how-to-animate-the-page-transition-in-next-js-68c7b888dce3?source=collection_archive---------3----------------------->

## 仅用五行代码在 Next.js 中制作页面转换动画。

![](img/11a241a9c5ad8db2257fa12b0c0d945d.png)

Photo by [Gabriela Palai](https://www.pexels.com/@gabriela-palai-129458?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/person-standing-on-brown-wooden-dock-395196/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

动画给你的应用程序带来了生命。今天我们将看看如何给 **Next.js** 应用程序页面转换添加动画。

# 工具

为此，我们将使用一个名为`[framer-motion](https://www.framer.com/motion/)`的奇妙的库。这个库被称为 React 的生产就绪动画库。

这个库的另一个优点是它完全支持服务器端渲染。因此，这将与 Next.js 理念完美契合

我们开始吧。

# 安装依赖项

首先，安装依赖项:

```
yarn add framer-motion
```

# 添加动画

现在转到你的`_app.tsx`文件，在顶部导入`motion`组件。

```
import { motion } from 'framer-motion'
```

接下来，使用下面的`motion.div`包装您的组件:

_app.tsx

这段代码将激活我们的初始页面加载。因为你包装了`Component`，所以它只会在你第一次加载页面时被触发。

但是我们希望每次页面切换都有动画，对吗？就这么办吧。

# 页面变化时的动画

我们知道页面的改变意味着`Nextjs`应用程序中路径的改变。所以我们将利用这个概念来使我们的页面生动起来。

我们将分解路由器组件，并为运动组件添加关键元素

_app.tsx

所以每当我们从一页到另一页时，路径都会改变。结果，`motion.div`的键也将改变，动画将被触发。

今天到此为止。祝您愉快！

```
***Get in touch with me via*** [***LinkedIn***](https://www.linkedin.com/in/56faisal/) ***or my*** [***Personal Website***](https://www.mohammadfaisal.dev/)***.***
```

[](/how-to-show-loader-on-page-changes-in-next-js-102edd0ec98d) [## 如何在 Next.js 中显示页面变化的加载器

### 让你的用户参与一个伟大的视觉反应！

javascript.plainenglish.io](/how-to-show-loader-on-page-changes-in-next-js-102edd0ec98d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***