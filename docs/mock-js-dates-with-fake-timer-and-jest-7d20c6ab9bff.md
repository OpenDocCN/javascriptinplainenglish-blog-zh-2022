# 用假计时器和笑话模拟 JavaScript 日期

> 原文：<https://javascript.plainenglish.io/mock-js-dates-with-fake-timer-and-jest-7d20c6ab9bff?source=collection_archive---------2----------------------->

## 当涉及日期时，更好地控制你的测试。

![](img/583b82cf4b1239d57310fa86b47ab6c9.png)

Photo by Bich Tran: [https://www.pexels.com/photo/white-and-black-weekly-planner-on-gray-surface-1059383/](https://www.pexels.com/photo/white-and-black-weekly-planner-on-gray-surface-1059383/)

有一段时间，Moment.js 允许我们避免使用 js 日期。但是，老实说，他们真的不怎么样。但是从那以后，JS 发展了很多，今天，日期 JS 对象是 Javascript 的未来。而 Moment.js 被弃用只是进一步证明了这一点。

当一些现代的不可变库还在包装自己的日期对象时。其他一些工具，比如 date-fns，只是一组更容易操作 JS 日期的工具。这意味着使用它们的方式会改变，测试它们的方式也会改变！

以前，我们可以很容易地模仿 moment 在被调用时返回一个特定的日期。然而，由于日期 JS 对象完全是 JS 运行时的一部分，所以没有办法模仿一个模块。不过 jest 团队想了想，给了我们一个解决方案:useFakeTimers。

# 为什么嘲笑时代

时间的主要问题是它从来都不是静止的。时间总是在变化，在你意识到这一点之前，你的测试会失败或者不可预测。这就是为什么你应该在测试时嘲笑你的时间，这样你就可以期待一个恒定的结果。

# 它是如何工作的

对于本文，我们假设您有一个安装项目(无论是 NodeJS 还是 Web，都没有关系)。

让我们编写一个简单的测试来打印`new Date()`的结果

```
describe('Testing date', () => {
  it('Should work', () => {
    const date = new ***Date***();
    ***console***.log(date);
  })
})
```

如果您运行此测试两次，结果会略有不同。那可不行。这就是为什么我们想要使用`useFakeTimer`将我们的测试从当前时间中分离出来。

让我们将它添加到我们的测试中

```
describe('Testing date', () => {
  it('Should work', () => {
    ***jest***.useFakeTimers();
    const date = new ***Date***();
    ***console***.log(date);
  })
})
```

现在，如果您运行您的测试，什么都没有改变，这是不幸的！实际上，使用假计时器是不够的，因为默认情况下，假计时器正在使用当前时间。我们想在此基础上使用`setSystemTime`来设置一个特定的时间

```
describe('Testing date', () => {
  it('Should work', () => {
    ***jest***.useFakeTimers();
    ***jest***.setSystemTime(new ***Date***('2020-02-19'));
    const date = new ***Date***();
    ***console***.log(date);
  })
})
```

瞧啊。现在，我们正在控制台中打印`2020–02–19T00:00:00.000Z`，我们的日期被嘲弄了！

> 请记住，您必须使用 IOS 字符串格式来创建新日期。

您不必做任何事情来“取消”日期，因为每个 jest 测试都是独立的。

就是这样！一篇非常短但(希望)有帮助的文章！希望你喜欢。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*