# 反应性能:使用状态惰性初始化

> 原文：<https://javascript.plainenglish.io/react-js-performance-usestate-lazy-initialization-ba475677fb6d?source=collection_archive---------13----------------------->

![](img/9ca87e4612b54c9b449e1557131404fc.png)

Photo by [Lautaro Andreani](https://unsplash.com/es/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每当你需要从一个返回值的函数中设置状态的初始值时(见下文)，该函数将在每次重新渲染时被调用，即使我们只在初始渲染时需要它。

```
const initialState = caluclateValue(props);const [someStateVal, setSomeStateValue] = React.useState(initialState);
```

我们可以用这样的函数延迟初始化 useState:

```
const getInitialState = (props) => caluclateValue(props);const [someStateVal, setSomeStateValue] = React.useState(initialState);
```

在这种情况下，React 只会在需要初始值的时候调用函数。那是在第一次渲染的时候。这被称为“惰性初始化”

玩玩它或者测试一下[这里](https://jsfiddle.net/shauryakalia/5anpb4Ld/42/)！

*最初发表于*[T5【https://www.shauryakalia.com】](https://www.shauryakalia.com/blogs/react-js-performance-use-state-lazy-initialization)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***