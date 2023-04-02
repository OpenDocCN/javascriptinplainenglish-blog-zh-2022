# 改进您的代码:今天就尝试这些 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/improve-your-code-try-out-these-javascript-features-today-c8116b718c49?source=collection_archive---------4----------------------->

## 尝试这些很酷的新特性，让你的代码变得更好。

![](img/93c970b126b52cbc503d346b335daaa5.png)

toptal.com

跟上前端社区的最新消息可能很难。事情发展得很快。新框架、新库、新特性等等。

我将尝试对 JavaScript 为前端开发人员准备的一些超级酷的新特性做一个简短的总结。

# 可选链接

可选链接是对该语言的一个很小但非常有用的补充。它使你必须写的代码更短更干净。它基本上允许您检查对象中是否存在值:

```
const someObject = {
  profile: {
   firstName: 'Nicky',
    lastName: 'Christensen',
    country: 'Denmark'
  }
}
// with optional chaining:
if (someObject?.profile?.firstName){ 
 console.log('Name is 1: ', someObject.profile.firstName)
}// navigate object graph safely// old style without optional chaining:
if (someObject && someObject.profile && someObject.profile.firstName){ 
 console.log('Name is 2: ', someObject.profile.firstName)
}// with optional chaining that fails as name doesnt exist:
if (someObject?.profile?.name){ 
 console.log('Name is 3: ', someObject.profile.firstName)
}// navigate object graph safely
```

正如您所看到的，打印出来的唯一两个 console.logs()是 ***"Name is 1"*** 和 ***"Name is 2"*** 。第三个没有打印出来，因为 ***【姓名】*** 在 ***【简介】*** 上不存在

在可选链接之前，我们必须像示例 2 那样做，这可能有点麻烦，而且编写起来很长。

# 无效合并

在 ECMAscript 的最新版本中，出现了一个新的逻辑运算符，当左边的操作数为空或未定义时，该运算符返回右边的操作数。你可以使用无效合并"？?"当需要设置默认值时。通常在这样做的时候，我们会使用“||”操作符，当然你仍然可以使用它。“那个？?"当你想避免副作用的时候，有一些其他的好处。

```
const falsy = false;
const emptyString = '';
const nullish = null;
const uDefined = undefined;console.log('1', falsy ?? 'Some string');
console.log('2', emptyString ?? 'Default string') //"" (as the empty string is not null or undefined)
console.log('3', nullish ?? 'Default string')
console.log('4', uDefined ?? 'Default string')console.log('-------');console.log('1.1', falsy || 'Some string');
console.log('2.2', emptyString || 'Default string')
console.log('3.3', nullish || 'Default string')
console.log('4.4', uDefined || 'Default string')
```

你可以试着在这把小提琴上弹奏它，所以||和之间的区别？？操作员:[https://jsfiddle.net/96b4zw71/](https://jsfiddle.net/96b4zw71/)

# 动态导入

ECMAScript 的最新版本在模块上引入了动态导入。这允许异步加载模块。这也被称为代码分割，我们已经通过构建工具做了很多年了。

```
let someAsyncModule = await import('/modules/my-module.ts');
```

# Promise.allSettled()

多年来，我们一直使用 Promise.all()来等待所有承诺得到解决。Promise.all()的问题是我们不知道哪些承诺实际上解决了，哪些承诺失败了。

promise.allSettled()方法允许您观察一组承诺的结果，无论它们是被履行还是被拒绝，这非常有用。

```
const promise1 = Promise.resolve("OK, I resolved");
const promise2 = Promise.reject("OH no, I was rejected");
const promise3 = Promise.resolve("After I was rejected");
Promise.allSettled([promise1, promise2, promise3])
    .then((results) => console.log(results))
    .catch((err) => console.log("error: " + err));
```

看看这把小提琴是如何使用的:[https://jsfiddle.net/x2h01z7p/1/](https://jsfiddle.net/x2h01z7p/1/)

# 扩展运算符

一段时间以来，我们有机会接触传播运营商。例如，当您想要合并数组或对象时，这尤其有用。在使用 spread 操作符之前，我们可以利用 array.concat 来合并数组，现在我们可以做得更简单:

```
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arr3 = [...arr1, ...arr2] //arr3 ==> [1,2,3,4,5,6]
```

对于对象，我们可以做:

```
const basePerson = {
 name: 'Nicky C',
  country: 'DK'
}const footballerPerson = {
 ...basePerson,
  team: 'Man UTD',
  shirtNumber: '11'
}console.log(footballerPerson) //Will output a merge of the two objects
```

试试这里:[https://jsfiddle.net/s86knh72/](https://jsfiddle.net/s86knh72/)

# 对象析构

通过利用对象重构，可以很容易地从对象中解包值

```
const basePerson = {
 name: 'Nicky C',
  country: 'DK'
}
const footballerPerson = {
 ...basePerson,
  team: 'Man UTD',
  shirtNumber: '11'
}const {team, shirtNumber} = footballerPerson;console.log(team, shirtNumber); //ManUtd, 11
```

试试这里:[https://jsfiddle.net/2z3rp18v/](https://jsfiddle.net/2z3rp18v/)

感谢阅读，我希望你喜欢这篇文章，如果是的话，请点击按钮或订阅来支持我。

如果你还不是一个中等成员，考虑成为一个！你可以从成千上万的作者那里获得像这样的好内容！它有助于支持作家，你也有机会通过写作赚钱。[**在这里注册每月只需 5 美元。**](https://nickychristensen.medium.com/membership)

***如果你想订阅我的全部内容，可以点击*** [***这里的***](https://nickychristensen.medium.com/subscribe)

[](https://blog.bitsrc.io/7-habits-of-highly-effective-developers-94abf02c1e05) [## 高效开发人员的 7 个习惯

### 提高效率和生产力的实用建议

blog.bitsrc.io](https://blog.bitsrc.io/7-habits-of-highly-effective-developers-94abf02c1e05) [](/how-to-become-a-great-developer-it-requires-more-than-being-able-to-write-code-d1f9e856f2dc) [## 如何成为一名优秀的开发人员——这需要的不仅仅是会写代码

### 成为一名优秀的开发人员不仅仅是写干净、好的代码！

javascript.plainenglish.io](/how-to-become-a-great-developer-it-requires-more-than-being-able-to-write-code-d1f9e856f2dc) [](https://medium.com/js-dojo/vue-3-tips-best-practices-54aec91d95dc) [## Vue 3 提示和最佳实践

### 我将分享我的知识，在使用 Vue 的最新版本 Vue3 时给你一些提示和最佳实践。

medium.com](https://medium.com/js-dojo/vue-3-tips-best-practices-54aec91d95dc) 

*如果你想找个时间和我聊聊，请关注我的*[*Twitter*](https://twitter.com/nickycdk)*|*[*LinkedIn*](https://www.linkedin.com/in/dknickychristensen/)*或者访问我的* [*网站*](https://nickychristensen.dk/) *。*

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**