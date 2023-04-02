# 用 JavaScript 写漂亮的代码会让你窒息

> 原文：<https://javascript.plainenglish.io/writing-pretty-code-in-javascript-can-choke-you-a1847865c6ce?source=collection_archive---------22----------------------->

![](img/e4437063b4116330237d07cc2dca0939.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

事实证明，如果不小心的话，还有更多方法可以扼杀 JavaScript。当然，我并不是说要有一个死循环。你可以在这里找到更多的。

```
const N = 10,000,000
const **v** = [0, 0]
const obj = {}console.time()
for (let i = 0; i < N; i++) {
  obj[**v**] = 0
}
console.timeEnd()
```

考虑一下上面的幼稚代码，我运行了 1000 万次。相信我，一千万不是一个大数目。当我将 Node.js 与其他语言进行比较时，例如。Rust，我通常不会看到明显的差异，直到它达到近 10 亿次运行。

做个猜测，上面的代码在我的电脑上需要 2.6 秒。这很难让人相信。`v`是一个数组，你怎么能把`v`作为对象的键呢？根据文档，`v`会在幕后为我投成一串，所以和`obj[v.toString()] = 0`差不多。是这样吗？

```
const N = 10,000,000
const **v** = [0, 0]
const obj = {}console.time()
for (let i = 0; i < N; i++) {
  obj[**v.toString()**] = 0
}
console.timeEnd()
```

再猜一个，上面的代码在我的电脑上需要 1.3 秒。所以`v`显然和`v.toString()`不一样。也许铸造需要努力决定铸造什么类型？可能吧，但是还是太久了，1 秒多。让我向你展示我期望得到的结果:

```
const N = 10,000,000
const obj = {}console.time()
for (let i = 0; i < N; i++) {
  obj[**0**] = 0
}
console.timeEnd()
```

我把`v`换成了固定的数字`0`。实际上，没有人会使用常量，但是我在这里只是测试性能，所以我不会使用随机数。猜测一下，这一块需要 23ms，比一个数递增 1000 万次(12ms)多一点。

## 失误？

是的，我确实犯了一个错误。感谢 Ski J 在[这里](/run-javascript-code-one-magnitude-faster-using-webassembly-448d470eb77d)指出。谁告诉你可以用一个物体做钥匙的？很有效，不是吗？我认为这是编写“漂亮”代码的捷径。是的，事实证明漂亮并不等同于高效——在这种情况下，远非高效，而是高效的反义词。现在我想知道我用 JavaScript 写的“漂亮”代码中有多少带有这种惊喜。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*