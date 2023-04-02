# KeyBoardAvoidingView 解释道。

> 原文：<https://javascript.plainenglish.io/keyboardavoidingview-explained-5ce75148151e?source=collection_archive---------9----------------------->

![](img/bc542acfc15afdbd0319f60feef13076.png)

今天我们将讨论 React Native 中的 KeyBoardAvoidingView。最近，我在我的个人项目中遇到了一个问题，我有一个表单，用户在 TextInput 中输入值，但是每当键盘打开时，TextInput 都留在键盘下面。我已经调查并找到了一个解决方案，代码如下:

你需要在 ScrollView 中使用键盘避免。在我的例子中，它工作得很好，另外一件事是你应该在键盘打开的时候更新 ScrollView。我用 useEffect 实现了这一点，我用键盘元素实现了这一点。最后一件事是，您应该为 ScrollView 设置一个 ref，它指示 ScrollView 包装的元素，以便 ScrollView 中的元素可以相应地移动。

那都是我送的。希望这篇文章对你有帮助:)

如果你想在 LinkedIn 上联系，请点击下面的链接。

[AKIN KARAYUN | LinkedIn](https://www.linkedin.com/in/akin-karayun-ab3239bb/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****