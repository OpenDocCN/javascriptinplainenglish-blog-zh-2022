# 7 个 JavaScript 一行程序看起来像个专家

> 原文：<https://javascript.plainenglish.io/7-javascript-one-liners-to-look-like-a-pro-1d6e5d42f3c4?source=collection_archive---------2----------------------->

![](img/31d709749ab44cfab09e1daf4206f39e.png)

大家好！👋

怎么了，朋友们？这里是**雪球**。我是一个年轻热情、自学成才的前端 web 开发人员，希望成为一名成功的开发人员。我喜欢用不同的技术构建 web 应用程序。

今天，我在这里给你一些好的 JS 一行程序，让你看起来像个专业人士。这些一行程序可能会对你的下一个项目有所帮助。我们走吧。🚀

# 切换布尔值

切换布尔，将**真**变为**假**，反之亦然。

```
const toggleBool = (val) => (val = !val)toggleBool(false) //true
```

# 随机布尔

生成一个随机布尔值。

```
const randomBool = () => Math.random() >= 0.5;randomBool() //true
```

# 滚动到顶部

滚动到页面顶部。

```
const scrollToTop = () => window.scroll(0,0)
```

# 检测黑暗模式

启用黑暗模式时返回 true。

```
const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
```

# 获取用户选择的文本

返回选定的文本。

```
const getSelectedText = () => window.getSelection().toString();
```

# 两个日期之间的差异

```
const dif = (d1, d2) => Math.ceil(Math.abs(d1.getTime() - d2.getTime()) / 86400000)dif(new Date("2006-02-24"), new Date ("2022-02-24"))
```

# 随机十六进制颜色

```
const hexColor = () => `#${Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, "0")}`;
```

这就是这篇文章，希望这篇文章对你有所帮助。欢迎在下面的评论中分享更多。
感谢您的阅读！

我在推特 [@codewithsnowbit](https://twitter.com/codewithsnowbit) 。跟着它走。

# 让我们连接🌏

*   [GitHub](https://github.com/codewithsnowbit)
*   [推特](https://twitter.com/codewithsnowbit)
*   [YouTube](https://www.youtube.com/channel/UCNTKqF1vhFYX_v0ERnUa1RQ?view_as=subscriber)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*