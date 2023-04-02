# SWE 面试问题，解释过了！

> 原文：<https://javascript.plainenglish.io/swe-interview-question-explained-3b2694319d9a?source=collection_archive---------22----------------------->

## 使用 Typescript

![](img/f62f31e03f1632eb4c1d1340546702cc.png)

假设我们正在为一家向全球饥饿人口运送苹果和香蕉的公司构建供应链管理应用程序。我们当前的目标是确定高效的交付要求。换句话说，应该向每个客户交付多少个箱子。继续之前，请注意以下几点:

一个饥饿的人可能会提出这样的请求:

*   *“我需要 250 根香蕉和 100 个苹果”*
*   *或者，“给我 100 个苹果和 100 个香蕉”*
*   *或者，“请给我 500 个苹果和 100 根香蕉！”*

***你可以假设对苹果和香蕉的需求是 50 的倍数*

接下来，请注意，可以使用 3 个箱子的组合进行交货:

1.  苹果盒(装有 50 个苹果)
2.  香蕉盒(装有 50 根香蕉)
3.  什锦盒(包含 100 个苹果，100 个香蕉)

任务如下:

**设计一个解决方案，根据一个饥饿的人的要求，计算出每个盒子应该送多少。该解决方案应使用尽可能少的箱子来满足交付要求(提示:优先考虑各种箱子！).**

## 解决办法

让我们首先定义一些类型，这将使问题更清楚。

```
interface HungerRequest {
  apples: number;
  bananas: number;
}interface DeliveryRequirements {
  AppleBoxes?: number;
  BananaBoxes?: number;
  AssortedBoxes?: number;
}
```

定义一些静态变量来表示每一个可能的投递箱也是有帮助的。

```
const AppleBox = { apples: 50 }
const BananaBox = { bananas: 50 }
const AssortedBox = { apples: 100, bananas: 100 }
```

接下来，让我们创建一个名为 *processHungerRequest* 的函数，它接受 *HungerRequest* 的实例作为参数，并返回 *DeliveryRequirements* 的实例。

```
const processHungerRequest = (hungerRequest: HungerRequest): *DeliveryRequirements* => {
  let { apples, bananas } = hungerRequest
  let deliveryRequirements: DeliveryRequirements = {}
  return deliveryRequirements;
}
```

到目前为止，我们已经定义了问题中描述给我们的所有参数。此外，我们已经实例化了一个功能，但它并没有做很多事情。现在让我们想出一个有效的解决方案来进行交付。

首先，这可能是一个好主意，按照提示所说的:*尽可能优先排序各种盒子。换句话说，我们应该尽可能多地使用各种各样的盒子。既然我们的函数行为是同步的，那就可以像计算有多少个可能的*组合框*这样的交付可以填充函数的开头。*

我们如何检查呢？一种方法是使用一个 *while* 循环来检查是否有足够的苹果和香蕉被请求使用另一个分类盒子。

```
while (apples >= AssortedBox.apples && bananas >= AssortedBox.bananas) {
  deliveryRequirements.AssortedBoxes = isUndefined(deliveryRequirements.AssortedBoxes) ? 1 : deliveryRequirements.AssortedBoxes + 1 
  apples = apples - AssortedBox.apples
  bananas = bananas - AssortedBox.bananas
}
```

* *注意: [*未定义*](https://lodash.com/docs/4.17.15#isUndefined) 是一个有用的 lodash 函数

上述代码的作用是:

1.  在苹果和香蕉请求的数量多于或等于*分类框*所能提供的数量的情况下循环。
2.  增加*交付要求*中*分类箱*的数量(如果未定义，则定义),因为我们知道至少还有 100 个苹果和 100 个香蕉需要交付。
3.  在增加了我们的*交付需求*之后，我们可以安全地将请求中的苹果和香蕉数量减少到真正剩余的数量。

该解决方案将安全有效地确定我们能为给定的*饥饿请求提供的*分类箱子*的最大数量。*

接下来，让我们编写一个类似的过程来完成订单的其余部分:

```
while (apples >= AppleBox.apples || bananas >= BananaBox.bananas) {
  if (apples >= AppleBox.apples){
    deliveryRequirements.AppleBoxes = isUndefined(deliveryRequirements.AppleBoxes) ? 1 : deliveryRequirements.AppleBoxes + 1
    apples = apples - AppleBox.apples
  }
  if (bananas >= BananaBox.bananas){
    deliveryRequirements.BananaBoxes = isUndefined(deliveryRequirements.BananaBoxes) ? 1 : deliveryRequirements.BananaBoxes + 1
    bananas = bananas - BananaBox.bananas
  }
}
```

让我们回顾一下这段代码的作用:

1.  在以下情况下循环:请求中剩余的苹果数量多于或等于 AppleBox 所能提供的数量，或者请求中剩余的香蕉数量多于或等于 BananaBox 所能提供的数量。在这种情况下，我们知道我们需要在交货中添加更多的这种类型的箱子。
2.  检查以上哪一个(哪些)条件适用，可能两个都适用，并增加相应的 *deliveryRequirements* 属性，减少相应水果(苹果或香蕉)的剩余数量。

3.这将持续到我们的整个订单完成，并且*交货要求*完成。

将这两个解决方案输入到我们的最终产品中，看起来会像这样:

请随意使用这个沙盒来亲自尝试一下:

 [## TS Playground——探索 TypeScript 和 JavaScript 的在线编辑器

### Playground 让你以一种安全和可共享的方式在线编写类型脚本或 JavaScript。

www.typescriptlang.org](https://www.typescriptlang.org/play?#code/PQKgBAlgtgDg9gJwC5gN6QM4FUB2ATAUwDMIcC8wBfMIhOKMAcgBs48BDDAC0YFgAoMCGACAxnBwYUEbPmKlyYALxgAFADd2zAFxh2OAJ4BKXZuaYwAVzkkyFJQD4wZ5UpXXCt8gIGkkBBCJ2UQIwAAlrAHMAgCUCAEdLAik0ATA9GBhmZN0cSygAIwCAbjSwAv1KjFz8ooRS-kpfHH9A4NCAEQJmCHUAgzjEiAQCKAIWjFTBMABBTOyAITgAD2SAfhrCkrKFypx2JdWMDbA8rfqymYwMRH88Q-XNuoam-jEJFLmsgkPlNAzvtUwABWAAMVHekhQu32+1+KnQFVhnF0YIh-HEUNm11u5Hh-3Y8xyYAAjKDQQAacp7FGk8noyEpGB0ELXCI4aIIQZJFIqVRcKKxBI8pC6dmc7nJJAmMBdHp9BADYXDUbjJCTRxTdLZFDoQmAqlIqpUP4CjlCxJSso6sCEeX9bkqsYTXRy3oO5UjZ3qv6oV7pADuXAg2TU+uykwcKiuN2QeJWADpw8kwAAyVPU5GR6M4uP3RNG-YYIxa9K27ruxWOr1qjAJmO4-NHP4yXCeBR4VR2ytKoY1ib13N3B7FsBrUlgXTdhW9yxO2uD2PDlYpgDUE7K6WTGoBEbAAFpsUv48sk0SMJvM8aVIXOAej43Dgnbxfpv6wEGQ6FVNuwFHZkST6-gAPsBV5Fn+KgwpUT4viWqCXhARBhuekEAd8QHnkYCHTGW5b2lWnqqgOXyLCuO6tjYHZdhWM7VsR6r1oB5EluOJKTvhPb0d6dakT85FgOuJKXluqEqL+h58ZhgKXu+6RIWoL5odBcIFjSxY4Xh6TTh6fYMXWKkHAJKiUe2dg0QRs7zgOhkjqxE5TrRulzv2jG2QJQkieBd43up97uaeL6yWU74jEglgIDgnF0URPEvD4GIfHA2QJqwkSqMycCshg4oWiKqh6ueugkmChrqboAAs9KUEYRiMslBCpXA6WZdluVcsKUoFbuxIVaV3lAgATNVtVAA) 

## 结论

这个问题可能有许多解决方案。我上面提供的是我使用起来很舒服的一个。我喜欢为我的眼睛和其他开发人员参考定义值。另外，你可能已经注意到我用了 [lodash 的“isUndefined”。如果你还没有使用它的话，可以看看这个很棒的库。你可能已经找到了不同的解决方案，如果是这样，我鼓励你分享它！](https://lodash.com/docs/4.17.15#isUndefined)

感谢阅读。如果你有什么要说或要问的，请点赞、分享和评论。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*