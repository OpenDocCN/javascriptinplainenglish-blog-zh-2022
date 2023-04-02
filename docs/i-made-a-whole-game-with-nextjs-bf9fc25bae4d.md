# 我如何用 Next.js 做了一个完整的“游戏”

> 原文：<https://javascript.plainenglish.io/i-made-a-whole-game-with-nextjs-bf9fc25bae4d?source=collection_archive---------10----------------------->

![](img/34091f9d8e2636d59761323ec98694da.png)

Photo by [Toby56](https://unsplash.com/@toby56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

嘿，用 Next.js 做游戏很有趣。最棒的是我不再挣扎。

当我正在进行某个 Ruby On Rails 项目时，我的兄弟突然带着这个非凡的想法出现了。

他是一个玩《我的世界》的 14 岁男孩，他喜欢玩这个游戏。我正要去他的房间，我知道他想在他用来提高《我的世界》PVP 技能的网络应用中增加一个功能。

是的，我开发了一个已经存在的想法，但是增加了两个特性。你可以称之为抄袭，但我称之为**修改**。

在了解了 web 应用程序的大致想法后，我问自己，我能用普通的 JavaScript 实现它吗？答案是，“是的！”

我再次问自己，我能用普通的 JavaScript 在**三天**内开发这个应用吗？答案是，“嗯，可能不会！”

最后，我想，“我可以用 Next.js 在三天内开发这个，”我坚定了这个选择。

在开始开发之前，我搜索了这个想法的相关域名，幸运的是，它是可用的，这让我超级兴奋。这种兴奋迫使我发展了这个想法。

我想到了将 Next.js 与 Tailwind CSS、plain CSS、FontAwesome 和一些自定义 SVG 图标一起使用。

我开始了一个 Next.js 项目。正如我以前说过的，我现在不能没有反应，老实说，那是真的。

## 这个想法

这个想法是建立一个可以计算点击速度和玩家 CPS 的网络应用。CPS[每秒点击次数]是一个度量用户点击鼠标或键盘按键次数的量。

## 万岁，开发完成了

所以，三天后，我开发了 web 应用程序，它仍然有一些小故障，因为我在使用`setInterval`，而`states`的变化正在烦人地执行`setInterval`。最后，我用一个名为 `[useInterval](https://www.30secondsofcode.org/articles/s/react-use-interval-explained)`的[定制钩子修复了它。](https://www.30secondsofcode.org/articles/s/react-use-interval-explained)

## 最后，部署

对于部署，我以前使用 AWS Lightsail 来开发我的全栈 Next.js web 应用程序，但这一次情况有所不同。从技术角度来说，这个 web 应用程序有点全栈，因为它使用了动态渲染和`getServerSideProps`，但从功能角度来说，它只是一个只有前端的 web 应用程序。

所以，我决定用 **AWS 放大**；我把我的 GitHub 和 Amplify 连接起来，附上回购协议，它就在网上，域名叫做[speedclicking.com](https://www.speedclicking.com/)

Amplify 最棒的一点是，你只需在本地环境中测试你的 web 应用，然后执行`git push`命令，推送之后，它会自动部署 web 应用。

同样的事情也是最糟糕的事情，因为每次部署都要花钱(0.01 美元/构建)。所以，我建议你创建两个 git 分支，一个叫做 main[用于 amplify],另一个叫做 development，用于 web 应用的开发阶段。

## 幸福的结局

结论是，你可以用 Next.js 和 Tailwind CSS 快速开发应用。你应该学习它，因为这是一个很好的技能，可能会让你的嘴里有一些面包，或者让你的大脑有一些多巴胺。

祝您愉快！

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。****