# 如何在用户用 react-query 输入后获取数据

> 原文：<https://javascript.plainenglish.io/how-to-fetch-data-after-user-input-with-react-query-b083d51b5d2d?source=collection_archive---------3----------------------->

![](img/a910274cfee5f1cae9f5e5ede5d9bd83.png)

Photo by Aditya Rathod on Unsplash

react-query 是 react 最广泛使用的查询包，它的大多数例子都描述了如何在组件挂载后立即运行查询，但是如果您想等到某个操作发生后再运行查询，该怎么办呢？

# 等到动作/输入发生后，再获取反应查询数据

在这个例子中，我们将只在用户在输入框中输入文本时获取数据，例如在搜索自动完成的情况下。

第一步:调用 useQuery 时，将“enabled”选项设置为 false。

在上面的代码中，inputValue 是存储用户提交的文本的状态变量。我们将它传递给 useQuery 的原因是让 react-query 知道查询响应数据依赖于该值(换句话说:该变量的不同值将返回不同的结果。这暗示了 react-query 如何缓存响应。)

步骤 2:使用“refetch”来实际执行查询。

步骤 3:观察返回数据的变化

上面的 useEffect()钩子监视返回的数据*和* is retrieving 变量。否则，如果返回的数据恰好是相同的(例如，对于一个相似的搜索字符串)，钩子将不触发。使用 is retrieving 作为依赖变量之一可以确保每次重新运行查询时都会触发 useEffect()挂钩。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***