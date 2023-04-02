# JavaScript 中 find()和 findIndex()的区别

> 原文：<https://javascript.plainenglish.io/difference-between-find-and-findindex-in-javascript-63204178bbc1?source=collection_archive---------4----------------------->

## JavaScript 中的 find() vs findindex():你需要知道的一切。

![](img/9c5d4f8b2af9376d484588914e563112.png)

Photo by [Safar Safarov](https://unsplash.com/@codestorm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 有很多有用的方法，我们可以用来实现我们开发中的某些操作。方法`find()`和`findIndex`是 JavaScript 中可以使用的两个数组方法。

因此在本文中，我们将通过介绍方法`find`和`findIndex`之间的区别来了解它们。让我们开始吧。

# 查找方法

方法`find()`用于返回通过某个测试函数的第一个数组元素。

find 方法接受一个函数作为它的参数，而函数本身接受三个参数:元素、索引和数组本身。

让我们看一个实际的例子:

```
let numbers = [2, 15, 18, 25];//using ES5
numbers.find(function(element) {
  return element >= 18;
}); //output: 18 //The same example using ES6
numbers.find(element => element >= 18); //output: 18
```

正如你在上面看到的，方法`find()`试图在数组中找到第一个大于或等于 18 的元素，然后返回它。

另外，记住 find 方法不会改变原始数组`numbers`。这里有一个例子:

```
console.log(numbers); //output: [2, 15, 18, 25]
```

如果数组中没有元素通过测试，方法`find()`返回`undefined`。此外，为了简单起见，我们在回调函数中只使用了一个参数，并将它作为参数传递给 find 方法。

# 方法 findIndex

方法`findIndex`用于返回通过某个测试函数的第一个数组元素的索引。

方法`findIndex`也接受一个回调函数，该函数可以接受三个参数(元素、索引和数组)。

这里有一个例子:

```
let numbers = [2, 10, 18, 25];//using ES5
numbers.findIndex(function(element) {
  return element > 2;
}); //output: 1 //The same example using ES6
numbers.findIndex(element => element > 2); //output: 1
```

正如您在上面看到的，方法`findIndex()`试图找到第一个大于 2 的元素的索引，然后返回它。数组中第一个大于 2 的元素是 10，其索引是 1。这就是为什么我们在输出中得到 1。

方法`findIndex()`也不改变数组。这里有一个例子:

```
console.log(numbers); //output: [2, 10, 18, 25]
```

如果数组中没有元素通过测试，方法`findIndex`也会返回`undefined`。

# 差异

方法`find()`与`findIndex()`非常相似。唯一的区别是 find 方法返回元素值，而 findIndex 方法返回元素索引。

# 结论

如你所见，方法`find()`和`findIndex`非常有用。第一个函数返回值，另一个函数返回索引。所以你需要两者，这取决于你想要达到的目标。

*感谢您阅读本文。此外，如果你觉得我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [*这里*](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得无限制的访问媒体上的所有文章，并支持我们作为作家。*

[](https://mehdiouss.medium.com/membership) [## 通过我的推荐链接加入 Medium-Mehdi Aoussiad

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mehdiouss.medium.com](https://mehdiouss.medium.com/membership) 

**更多阅读:**

[](/8-javascript-features-to-know-before-learning-reactjs-aac8b7748b30) [## 学习 React 之前应该了解的 JavaScript 特性

### 在做出反应之前，先学习这些 JavaScript 特性

javascript.plainenglish.io](/8-javascript-features-to-know-before-learning-reactjs-aac8b7748b30) [](/9-awesome-css-properties-that-you-probably-have-never-used-8cc4c385c3c6) [## 你可能从未用过的 9 个很棒的 CSS 属性

### 非常有用和有趣的 CSS 属性，你应该知道。

javascript.plainenglish.io](/9-awesome-css-properties-that-you-probably-have-never-used-8cc4c385c3c6) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。****