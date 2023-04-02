# React“穷尽式深度”埃斯林规则访谈

> 原文：<https://javascript.plainenglish.io/interview-with-reacts-exhaustive-deps-eslint-rule-21ccc292a3f9?source=collection_archive---------9----------------------->

![](img/69ac010d20b7df26b4e04d4d8bd412bd.png)

Sebastian: 你能简单介绍一下你自己吗？你是做什么的？

**exhaustive-deps:** 我是林挺规则，在 React 钩子中捕捉丢失的依赖项。我可以出现在任何有依赖关系的钩子上，但是人们通常在 useEffect、useCallback 和 useMemo 上看到我。

**Sebastian:** 那么,*成为一条棉绒规则感觉如何？*

**exhaustive-deps:** 感觉挺放松的。你只要做好自己的工作，就会有某种满足感。我确实有点洁癖，但我想这是我的一部分。

老实说，做代码感觉有点奇怪。但是不要告诉其他 lint 规则。

**Sebastian:** 怎么看待这么多人加“*//eslint-disable-next-line react-hooks/exhaustive-deps”*禁用你？

**exhaustive-deps:** 挺不幸的。显然，问题的根源是开发人员没有完全意识到我想要达到的目的。

当然，我有时会有点烦人，但我的意图总是好的。我相信 React 用户有责任阅读文档并遵循推荐的方法来使用依赖关系数组。

如果他们不想阅读文档，他们可以随时和我交谈，我可以提供指导。每月只需 10 美元，他们就可以与 React 生态系统中的所有其他工具交流，比如我的兄弟“react-hooks/rules-of-hooks”

我有洁癖。我居住在每一个苏美尔扫帚。我什么都见过，从周日下午洗涤剂瓶的狂欢到宇宙将成为永恒污垢的日子。

>访问结束，退出代码为 1。

>第 22 行出错:React 挂钩“useInterview”缺少依赖项。要么包含它，要么移除依赖项数组。

*感谢阅读！如果你喜欢这些幽默的科技故事，并想支持我永远坚持写作，可以考虑* [*报名成为一名中等会员*](https://sebastiancarlos.medium.com/membership) *。每月 5 美元，你可以无限制地阅读媒体上的故事。如果你* [*用我的链接*](https://sebastiancarlos.medium.com/membership) *注册，我会赚一小笔佣金。也可以关注我的* [*中*](https://sebastiancarlos.medium.com/) *和* [*推特*](https://twitter.com/5ebastiancarlo5) *。*

[](https://sebastiancarlos.medium.com/membership) [## 加入我的介绍链接媒体-塞巴斯蒂安卡洛斯

### 阅读塞巴斯蒂安·卡洛斯(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接…

sebastiancarlos.medium.com](https://sebastiancarlos.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*