# 通过承诺来提升你的 JavaScript 技能

> 原文：<https://javascript.plainenglish.io/level-up-your-skills-in-javascript-with-the-inclusion-of-promises-5a2c84f2fe71?source=collection_archive---------8----------------------->

## JavaScript 中的承诺是什么？这是一段可能在某个时间点产生一个值的代码。

![](img/dd011be5228e2c244dbe45296e311aa3.png)

[Photo by Valerie Voila from Pexels](https://www.pexels.com/photo/island-landscape-13727429/)

如果你现在写 JavaScript，你最终会听到或读到所谓的`asynchronous`代码。JavaScript 最初是以同步方式构建的，简而言之，这意味着它以编写代码的方式运行:

```
console.log('a');
console.log('b');
console.log('c');// Output: a b c
```

这将按照准确的顺序输出。异步代码可以用我们关心的方式编写。如果我们想要一个特定的顺序，我们可以这样做:

```
console.log('a');setTimeout(() => { console.log('b') }, 2000);console.log('c');// Output: a c b
```

正如你所看到的，使用异步代码，我们可以更好地控制代码的顺序。我们可以让事情以我们真正关心的方式运行。今天，我们将讨论承诺的概念！

# 承诺()

简而言之，承诺是一段代码，可以在某个时间点产生一个值。在任何给定时间，承诺可能处于三种状态之一:待定、履行或拒绝。承诺取代了编写回调的需要，与传入的回调不同，承诺有一些保证:

*   当通过`then()`关键字添加回调时，在当前运行完成之前，这些回调永远不会被调用。本质上，如果我们有 3 个步骤，第 2 步将不会开始，直到第 1 步已经完成。
*   即使添加了异步操作的成功或失败，也会调用回调。
*   您可以添加任意数量的`then()`，它们将按照接收的顺序被调用。

这方面的一个例子如下(我们将在下面进一步讨论带有箭头功能的版本):

```
firstFunction()
  .then(function (firstResult) {
    return secondFunction(firstResult);
  })
  .then(function (secondResult) {
    return thirdFunction(secondResult);
  })
  .then(function (thirdResult) {
    console.log(`Result: ${thirdResult}`);
  })
  .catch(theFailingCallback);
```

这是无限优于老学校回调地狱，这是下面

```
firstFunction (function (firstResult) {
  secondFunction (firstResult, function (secondResult) {
    thirdFunction (secondResult, function (thirdResult) {
      console.log (`Result: ${thirdResult}`);
    }, theFailingCallback);
  }, theFailingCallback);
}, theFailingCallback); 
```

使用像承诺这样的现代方法，我们将回调附加到返回的承诺上，这形成了一个承诺链。我们还可以使用箭头函数来编写我们的承诺链，如下所示:

```
**Example 1 (Arrow function with explicitly used return keyword)**firstFunction()
  .then((firstResult) => {return secondFunction(firstResult)})
  .then((secondResult) => {return thirdFunction(secondResult)})
  .then((thirdResult) => {console.log(`result: {thirdResult})})
  .catch(theFailingCallback); 
```

或者

```
**Example 2 (Arrow function without explicitly used return keyword)**firstFunction()
  .then((firstResult) => secondFunction(firstResult))
  .then((secondResult) => thirdFunction(secondResult))
  .then((thirdResult) => console.log(`result: {thirdResult}))
  .catch(theFailingCallback);
```

> 重要提示:一定要返回结果，否则回调不会捕捉到之前承诺的结果(对于箭头函数，`() => x`是`() => { return x; }`的简称)。如果前一个处理程序开始了一个承诺，但没有返回，就没有办法再跟踪它的结算，这个承诺就被称为“浮动的”。
> — [MDN 网络文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

如果存在类似竞态条件的情况，这尤其糟糕。如果来自前一个处理程序的承诺从未正确返回，那么下一个承诺中的处理程序将被提前调用，并且值可能不完整。如果可以的话，我们希望不惜一切代价避免这种情况

如果需要，您可以在 catch 语句后链接一个 then，即使承诺失败，该语句也会执行:

```
firstFunction()
  .then((firstResult) => {return secondFunction(firstResult)})
  .then((secondResult) => {return thirdFunction(secondResult)})
  .then((thirdResult) => {console.log(`result: {thirdResult})})
  .catch(theFailingCallback)
  .then((fourthResult) => {console.log(`do this {fourthResult})}; 
```

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) [## Promise - JavaScript | MDN

### Promise 对象表示异步操作的最终完成(或失败)及其结果…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 

# Promise.all()

promise.all()函数接受一系列承诺。返回值是一个单独的数组，它将包含从传入的承诺中返回的值。但是，如果这些值中的任何一个被拒绝，promise.all()会立即被拒绝。这方面的一个例子如下:

```
const firstPromise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('1'), 1000);
});const secondPromise= new Promise((resolve, reject) => {
  setTimeout(() => resolve('2'), 2000);
});Promise.all([firstPromise, secondPromise]).then((returnedValues) => console.log(returnedValues)); // Output: Array ["1", "2"]
```

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) [## Promise.all() - JavaScript | MDN

### Promise.all()方法接受一个可迭代的承诺作为输入，并返回一个解析为…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) 

虽然我知道这只是对 JavaScript 前景的一个非常简要的概述，但我强烈建议更深入地了解一下。这确实感觉像一个兔子洞，但它是最有价值的概念之一，值得学习和充分理解。我在过去的福特和福克斯体育工作中使用过这些概念，一旦我开始理解和编写异步代码，我就像这样

![](img/ac5e4eac95d3242d1b563d309ef06b66.png)

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。

如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于[内置 JavaScript 函数](https://medium.com/javascript-in-plain-english/level-up-your-javascript-skills-with-these-built-in-functions-a15607b72c2b)的文章，用 React 、[设置](/developing-custom-themes-for-shopify-getting-started-b137407c0cb7) [Firebase，为 Shopify](/use-a-firebase-db-inside-your-reactjs-project-2cfb56b51162) 、[基于类的 React 组件](/class-based-components-in-react-14335f0ee539)和[获取 API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 进行定制主题开发。

感谢您的阅读，祝您愉快！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***