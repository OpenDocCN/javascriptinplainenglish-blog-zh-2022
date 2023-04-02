# Promise 会存储响应吗？

> 原文：<https://javascript.plainenglish.io/does-promise-store-the-response-85edc896ca7f?source=collection_archive---------22----------------------->

![](img/692a14b175f2e8b1545a71c9b945a69d.png)

Photo by [Ester Marie Doysabas](https://unsplash.com/@estersthetic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常使用 Promise，用它来获取 API 调用相当简单。但是你有没有想过在它结束后会发生什么，我的意思是你在以后的时间里会回到一个完成的承诺吗？如果是的话，你打算用它做什么？

## 承诺，常见用法

让我们来看一个常见用法的快速示例:

```
const p = new Promise(resolve => { 
  console.log('resolve')
  resolve('data') 
}) 
```

一个`p`持有一个马上解决的承诺。为了监听响应，我们使用了`then`:

```
p.then(v => { 
  console.log('first then', v) 
})
```

打印结果应该如下所示:

```
resolve
first then data
```

到目前为止非常简单。

## 以第二种决心许诺

假设现在我们继续握住`p`的手柄，以后再用:

```
setTimeout(() => {
  p.then(v => {
    console.log('second then', v)
  })
}, 3000)
```

在我们再次听到承诺之前，我们等待 3 秒钟，这时我们知道第一个决心已经结束了。在你看到下面的屏幕输出之前，你能猜一下吗？

```
resolve
first then data
second then data 
```

是的。由于承诺不需要时间来解决，它完成第一个`then`，三秒后完成第二个`then`。

你注意到一些有趣的事情了吗？当我们将 resolve 消息放入 Promise 中时，每次 Promise 解析时，它都会打印一条“resolve”消息。但是在我们的案例中它打印了多少次呢？

我们在“先有数据”之前看到它。然而，在“秒然后数据”之前没有第二个“解决”消息。怎么会这样

## 承诺并保存回复

哦，那是因为我们的承诺已经完成，在我们的情况下解决；所以响应数据不应该再改变了。它只是返回第一次保存的数据，并立即返回给您，甚至不执行任何与最初承诺相关的操作。

哈，这意味着 Promise 不仅仅是一个传递代码，就像`init->start->then`一样，它为`response`和`error`提供了内置存储。否则以后就不能用了。

好吧，这一切对我们意味着什么？意思是**只要使用原来的 Promise 对象**就不会意外触发第二次 API。API 说，木已成舟。

这个就用一个真实的例子来说吧。假设您有两个组件，都使用来自相同 API 的相同响应数据，您可能会考虑使用一个全局变量来保存响应数据，以便两个组件可以使用相同的数据集。因为承诺的本质，你可以在这两个部分之间分享承诺。据我们所知，无论哪一个`then`先完成，另一个都会从已经返回的响应中得到它，而不需要额外的努力。整洁吗？

可以随意玩上面的演示。我给你另一个作业，如果我们对两个`then`都等待 3 秒，我们会得到相同的行为吗？请去玩得开心。

## 源代码

我发现了一份我不久前写的《无极》的副本，所以也许这可以揭示更多里面发生了什么。

```
// Solved at 8/7/2022
// This version supports async nature of promise
// however this one doesn't support promise return from then
class MyPromise {

  constructor(fn) {
    this.state = 'pending'
    this.value = null
    this.resolveCbs = []
    this.rejectCbs = []

    const resolve = v => {
      if (this.state === 'pending') {
        this.state = 'fulfilled'
        this.value = v
        this.resolveCbs.forEach(cb => cb())
      } 
    }

    const reject = v => {
      if (this.state === 'pending') {
        this.state = 'rejected'
        this.value = v
        this.rejectCbs.forEach(cb => cb())
      }
    }

    try {
      fn(resolve, reject)
    } catch (e) {
      reject(e)
    }
  }

  then(resolve, reject) {
    return new MyPromise((_resolve, _reject) => {
      const resolveFn = () => {
        if (!resolve) _resolve(this.value)

        queueMicrotask(() => {
          try {
            _resolve(resolve(this.value))
          } catch (e) {
            _reject(e)
          }
        })
      }
      const rejectFn = () => {
        if (!reject) return _reject(this.value)

        queueMicrotask(() => {
          try {
            _resolve(reject(this.value))
          } catch (e) {
            _reject(e)
          }
        })
      }

      if (this.state === 'pending') {
        this.resolveCbs.push(resolveFn)
        this.rejectCbs.push(rejectFn)
      } else if (this.state === 'fulfilled') {
        resolveFn()
      } else if (this.state === 'rejected') {
        rejectFn()
      } 
    })
  }

  catch(reject) {
    return this.then(null, reject)
  }
}

// Do not edit the line below.
exports.MyPromise = MyPromise;
```

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[*YouTube****，以及***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*