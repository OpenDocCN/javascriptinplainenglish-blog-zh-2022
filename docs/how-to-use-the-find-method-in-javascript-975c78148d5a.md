# 如何在 JavaScript 中使用 find()方法

> 原文：<https://javascript.plainenglish.io/how-to-use-the-find-method-in-javascript-975c78148d5a?source=collection_archive---------3----------------------->

## 使用 find()数组辅助方法的教程

![](img/a005a913bc031cecf08819eb42bf1670.png)

## 介绍

我最近写了一些关于使用 [map()](https://blog.devgenius.io/using-map-in-javascript-94e6050299e6) 和 [forEach()](/how-to-use-the-javascript-foreach-method-a9e6f9e9a071) 数组助手方法的文章。在本文中，我们将看看`find()`方法。过去，在 ES6 之前，如果我们想从数组中找到匹配特定内容的元素，我们可以使用一个`for`循环。让我们看看如何从字符串数组中找到字符串“apple”。

```
const fruits = ["Fig", "Orange", "Lemon", "Apple", "Kiwi"];let fruit;for(let i = 0; i < fruits.length; i++) {
  if(fruits[i] === "Apple") {
    fruit = fruits[i];
    break;
  }
}console.log(fruit);
```

在上面的例子中，我们首先使用一个名为 *fruits* 的常量来声明一个变量。我们给它分配一个包含各种水果串的数组。接下来，我们使用`let`创建一个名为 *fruit* 的变量，我们将在一个`for`循环中使用它。我们创建一个标准的`for`循环，它将遍历*水果*数组。在循环内部，我们创建一个`if`语句，如果水果元素与字符串 *Apple* 匹配，我们将*水果*变量设置为等于 *Apple* 。如果它与字符串 *Apple* 匹配，那么我们也将跳出`for`循环，因为在我们达到匹配后，继续遍历水果数组是没有意义的。我们接着`console.log` *水果*因为水果数组包含*苹果*我们可以看到我们的*水果*变量已经被设置为*苹果*。

## 使用查找()

这是可行的，但要实现我们找到苹果元素的目标，还有很长的路要走。数组助手方法`find()`帮助我们实现同样的结果，但是要容易得多。

通过使用`find()`方法，我们可以返回给定数组中第一个(并且只有第一个元素)元素的值，该值与我们传入的回调函数的结果相匹配。然后，该方法将返回元素。当我们使用`find()`时，回调函数必须返回一个布尔值(真或假)。当我们调用`find()`方法时，它将对数组中的每个元素运行一次，但是当它找到一个匹配时，它将停止运行并返回元素的值。澄清一下，即使我们使用的数组有多个匹配，只有第一个返回 true 的元素会被返回，其他元素不会被运行。让我们重新实现最初的例子，但是这次使用`find()`。

```
const fruits = ["Fig", "Orange", "Lemon", "Apple", "Kiwi"]; let fruit = fruits.find(function(fruit) {
  return fruit === "Apple";
})console.log(fruit);
//Returns ---> Apple
```

在上面的例子中，在我们创建了*水果*数组之后，我们创建了一个*水果*变量。我们将使用`find()`的结果赋给*水果*变量。我们在*水果*数组上调用`find()`方法，并使用匿名回调函数设置*水果*参数。每次`find()`运行时，*水果*参数将代表来自*水果*数组的单个*水果*元素。如果元素等于字符串*苹果*，我们返回*水果*。当我们`console.log`水果*的返回值*时我们可以看到它已经被设置为苹果*苹果*。如果*水果*数组不包含*苹果*，那么将返回 undefined，如下例所示:

```
const fruits = ["Fig", "Orange", "Lemon", "Kiwi"];let fruit = fruits.find(function(fruit) {
  return fruit === "Apple";
})console.log(fruit);
//Returns ---> undefined
```

## 嵌套数据结构

如果我们使用包含用户的对象的嵌套数据结构，我们也可以使用`find()`。让我们看一个例子，我们有三个用户，我们想返回第一个在测试中得分为零的用户的名字。

```
const results = [
  {
    name: "Billy",
    score: 90
  },
  {
    name: "Ted",
    score: 100
  },
  {
    name: "Laura",
    score: 9
  },
  {
    name: "Alice",
    score: 100
  },
  {
    name: "Peter",
    score: 98
  }
];let winner = results.find(function(result) {
  return result.score === 100;
});console.log(winner.name);
//Returns ---> Ted
```

在上面的例子中，我们创建了一个名为 *results* 的变量，并为其分配了一个数组，该数组包含名为*名为*和*分数为*的对象。我们创建了一个名为 *winner* 的变量，并将对 *results* 数据结构使用`find()`方法的结果赋给这个变量。我们设置参数 *result* ，它将代表我们的结果数组中的每个对象。如果对象的*分数*等于 100，我们将返回结果。

第一个包含 100 分的对象拥有用户*泰德*。我们`console.log` 了这个对象的*名*，所以我们得到了返回的 *Ted* 。由于我们使用的是 ES6，所以我将用一个例子来完成这篇文章，这个例子使用一个带有隐式返回(不使用 return 关键字)的箭头函数来完成上面的`find()`方法。

```
const results = [
  {
    name: "Billy",
    score: 90
  },
  {
    name: "Ted",
    score: 100
  },
  {
    name: "Laura",
    score: 9
  },
  {
    name: "Alice",
    score: 100
  },
  {
    name: "Peter",
    score: 98
  }
];let winner = results.find(result => result.score === 100);console.log(winner.name);
//Returns ---> Ted
```

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***