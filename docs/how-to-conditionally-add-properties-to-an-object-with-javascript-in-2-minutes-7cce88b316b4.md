# 如何在 2 分钟内用 JavaScript 有条件地向对象添加属性

> 原文：<https://javascript.plainenglish.io/how-to-conditionally-add-properties-to-an-object-with-javascript-in-2-minutes-7cce88b316b4?source=collection_archive---------12----------------------->

您是否曾经遇到过想要有条件地给对象添加属性的情况？有几种方法可以实现这一点。在本文中，我将深入研究并向您展示几个方法来做到这一点。

![](img/915fba325773751b0884527e33cda40d.png)

# 示例 1

我想向你展示的第一种方法几乎可以实现我猜想你想要实现的目标。考虑下面的代码。

```
let firstName = 'Nicky';
let lastName = 'Christensen';
let country = 'Denmark';
let age;
let emptyString = '';const myObject = {
 firstName: firstName ? firstName: undefined,
  lastName: lastName ? lastName : undefined,
  country: country ? country : undefined,
  age: age ? age : undefined,
  someString: emptyString ? emptyString : undefined
}console.log('two', myObject)
```

看着上面的代码，你认为输出会是什么？如果您猜测它会将所有属性添加到对象中，那么您是正确的。

```
{
    "firstName": "Nicky",
    "lastName": "Christensen",
    "country": "Denmark",    
    "age": undefined,
    "someString": undefined
}
```

如你所见，这不是我们 100%想要达到的目标。仍然会添加属性，只是没有值的变量的值为 undefined。这不是我们想要实现的目标，尽管已经很接近了。

让我们试着看一个更正确的例子。

# 示例 2

正如标题中提到的，我们希望有条件地向对象添加属性。考虑以下代码:

```
let firstName = 'Nicky';
let lastName = 'Christensen';
let country = 'Denmark';
let age;
let emptyString = '';const myObject = {
  ...(firstName && {firstName: firstName}),
  ...(lastName && {lastName: lastName}),
  ...(country && {country: country}),
  ...(age && {age: age}),
  ...(emptyString && {someString: emptyString})
}console.log(myObject);
```

您可能注意到，我们可以检查变量是否有值，如果变量包含值，我们就在 myObject 对象上创建一个属性

你觉得上面的代码会输出什么？如果你猜对了下面显示的内容，你就对了。

```
{
    "firstName": "Nicky",
    "lastName": "Christensen",
    "country": "Denmark"
}
```

这正是我们想要实现的目标。可以看到，我们的对象不像以前那样包含属性( ***年龄*** & ***某串*** )。

# 最后一个例子

除了做您在示例 2 中看到的事情，您实际上还可以利用 Object.assign()做一些我们在示例 2 中做的事情。
让我们试着看一看:

```
......const myObjectThree = {}Object.assign(myObjectThree, 
  firstName && { firstName: firstName },
  lastName && { lastName: lastName },
  country && { country: country },
  age && { age: age },
  emptyString && { someString: emptyString }
);

console.log('three', myObjectThree)
```

这就是了。在 Javascript 中有条件地向对象添加属性的一些简单方法:

感谢阅读，我希望你喜欢这篇文章，如果是的话，请点击按钮或订阅来支持我。

附注:首先，你应该收到我的邮件。 [***在这里做*** *！*](https://nickychristensen.medium.com/subscribe)

*其次，如果你自己喜欢体验媒介，可以考虑通过注册会员* *来支持我和其他成千上万的作家* [***。***](https://nickychristensen.medium.com/membership) *它每个月只花****【5****美元，它极大地支持了我们，作家，你也有机会用你的写作赚钱。通过这个链接* *报名* [***，你就直接用你的一部分费用支持我，不会多花你多少钱。如果你这样做了，万分感谢。***](https://nickychristensen.medium.com/membership)

[](https://blog.bitsrc.io/7-habits-of-highly-effective-developers-94abf02c1e05) [## 高效开发人员的 7 个习惯

### 提高效率和生产力的实用建议

blog.bitsrc.io](https://blog.bitsrc.io/7-habits-of-highly-effective-developers-94abf02c1e05) [](https://medium.com/the-side-hustle-club/7-side-hustles-you-can-do-to-earn-passive-income-online-a2d17bf29558) [## 你可以做 7 个侧面的生意来赚取网上的被动收入

### 寻找这样的方法来赚取一些额外的钱，从长远来看，没有花费大量的时间？这里有一些…

medium.com](https://medium.com/the-side-hustle-club/7-side-hustles-you-can-do-to-earn-passive-income-online-a2d17bf29558) [](https://medium.com/js-dojo/vue-3-tips-best-practices-54aec91d95dc) [## Vue 3 提示和最佳实践

### 我将分享我的知识，在使用 Vue 的最新版本 Vue3 时给你一些提示和最佳实践。

medium.com](https://medium.com/js-dojo/vue-3-tips-best-practices-54aec91d95dc) 

如果你想找个时间和我聊聊，可以关注我的 [*推特*](https://twitter.com/nickycdk)*|*[*LinkedIn*](https://www.linkedin.com/in/dknickychristensen/)*或者直接访问我的* [*网站*](https://nickychristensen.dk/) *。*

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*