# JavaScript: forEach 和 Async/Await 已正确完成

> 原文：<https://javascript.plainenglish.io/javascript-foreach-and-async-await-done-correctly-49cc04a3df04?source=collection_archive---------8----------------------->

![](img/ba5e6c2d8200af63f1830c3aa82ad088.png)

如果您曾经尝试过在 arr.forEach 中使用 async/await，您可能会发现您的应用程序中有一些奇怪的和意想不到的副作用。

这主要是因为 arr.forEach 期望同步函数，而不是异步函数。这个基本上意味着它不会像你所期望的那样“等待”。

考虑下面的代码

```
async function someAsyncFunction(value) {
 //Simulate a promise that returns a value
  const randomDelay = Math.random() * (100 - 10) + 10;
  setTimeout(() => console.log(value), randomDelay);
}const values = [100, 200, 300];
values.forEach(async (val) => {
  await someAsyncFunction(val);
});
```

最初，您会期望输出

```
100
200
300
```

但是运行几次代码，您会遇到不同的输出。

# 如何解决问题

既然你已经看到了像上面这样做的奇怪的怪癖，你实际上怎样才能正确地做呢？让我们来看看

# Promise.all()

我发现正确做这件事的最好和最干净的方法是使用 ***Promise.all()*** 。以下代码将产生您所期望的结果:

```
async function someAsyncFunction(value) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`Promise resolved`)
    }, 100)
  })
}
const values = [100, 200, 300];
const testFunction = async () => {
 return await Promise.all(
    values.map(async (val) => {
      return await someAsyncFunction(val);
    })
  );
}const run = async () => {
  const test = await testFunction();
  console.log(test);
}run();
```

你可以在这里找到代码:[https://jsfiddle.net/xbkevnfz/](https://jsfiddle.net/xbkevnfz/)

感谢阅读，我希望你喜欢这篇文章，如果是的话，请点击按钮或订阅来支持我。

如果你还不是一个中等成员，考虑成为一个！你可以从成千上万的作者那里获得像这样的好内容！它有助于支持作家，你也有机会通过写作赚钱。[**在这里注册每月只需 5 美元。**](https://nickychristensen.medium.com/membership)

***如果您想订阅我的所有内容，*** [***您可以在这里做***](https://nickychristensen.medium.com/subscribe)

[](/stop-using-momentjs-for-dates-this-is-the-better-alternative-2709afb229a0) [## 停止使用 Moment.js 来表示日期——这是更好的选择

### 在 JavaScript 中使用 Date 对象可能会非常麻烦！如果你没有使用现成的数据库，你可以…

javascript.plainenglish.io](/stop-using-momentjs-for-dates-this-is-the-better-alternative-2709afb229a0) [](https://blog.bitsrc.io/10-things-tips-i-would-tell-my-younger-self-as-a-frontend-developer-and-a-human-being-7959fb8eaf96) [## 作为开发人员，我会给年轻时的自己 10 个建议

### 作为一名前端开发人员和一个普通人，我会给自己的 10 样东西！

blog.bitsrc.io](https://blog.bitsrc.io/10-things-tips-i-would-tell-my-younger-self-as-a-frontend-developer-and-a-human-being-7959fb8eaf96) [](https://medium.com/front-end-weekly/a-closer-look-on-array-reduce-with-useful-examples-34f222664e66) [## 通过有用的示例进一步了解 array.reduce()

### 提高您的 javascript 技能，并通过一些有用的示例学习如何使用 Array.prototype.reduce()

medium.com](https://medium.com/front-end-weekly/a-closer-look-on-array-reduce-with-useful-examples-34f222664e66) [](/typescript-generics-explained-in-2-minutes-c95e49783347) [## 用 2 分钟的时间用例子解释了类型脚本泛型

### 深入探究类型脚本泛型

javascript.plainenglish.io](/typescript-generics-explained-in-2-minutes-c95e49783347) 

***如果你想找个时间和我聊聊，请关注我的***[***Twitter***](https://twitter.com/nickycdk)***|***[***LinkedIn***](https://www.linkedin.com/in/dknickychristensen/)***或者直接访问我的*** [***网站***](https://nickychristensen.dk/) ***(丹麦文)***

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。**