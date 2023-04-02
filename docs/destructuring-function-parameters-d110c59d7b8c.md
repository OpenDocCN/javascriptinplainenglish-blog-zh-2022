# 在 JavaScript 中析构函数参数

> 原文：<https://javascript.plainenglish.io/destructuring-function-parameters-d110c59d7b8c?source=collection_archive---------3----------------------->

## 初学者析构函数参数入门

![](img/fe112a49b27f88f70035f9b2e75cc9bc.png)

我最近发表了三篇关于[数组](/array-destructuring-in-javascript-c79b747dd864)析构、[对象](/basic-object-destructuring-in-javascript-7c4538ec70ec)析构以及从[嵌套](/nested-destructuring-in-javascript-3fe186b1d34e)对象析构的文章。析构可以用在函数定义的括号内(放置参数的地方)，以便从传递给函数的参数中挑选出值。当您只想在函数中使用某个对象的某些属性时，这非常有用。使用什么类型的函数并没有什么区别，但是我们将看一个使用箭头函数的例子。

## 析构对象

为了在函数的参数中析构一个对象，我们在函数的括号中放置了一组花括号。在花括号内，我们放置我们想要挑选的对象的属性。下面是一个使用箭头函数的例子。

```
const drinks = {
  cola: 2,
  lemonade: 1,
  milk: 3,
  tea: 2,
  coffee: 2,
  wine: 8
};const hotDrinksPrices = ({ tea, coffee }) => {
  return tea + coffee;
}hotDrinksPrices(drinks);//Returns ---> 4
```

在上面的例子中，我们有一个名为*饮料*的对象，它包含一些饮料和价格。接下来，我们创建一个名为 *hotDrinksPrices* 的箭头函数。在函数内部，我们想要返回来自*饮料*对象的*茶*和*咖啡*属性的值的总和。为了挑选出*茶*和*咖啡*属性，我们在函数的参数中使用花括号，并挑选出*茶*和*咖啡*属性。当函数运行时，我们将整个*饮料*对象作为参数传入。

## 析构数组

虽然函数参数内部的析构最常用于对象，但是当我们将数组传递给函数时，也可以使用相同的方法。唯一的区别是，在函数的圆括号中，我们将想要挑选的项目放在一个数组中。顺序在这里很重要，就像我们在函数参数之外执行数组析构一样。如果我们想跳过一个元素，那么我们可以使用逗号。让我们看一个例子。

```
const names = ["Frank", "Luke", "Ben", "Tony", "Pete"];const printName = ([, secondName, thirdName ]) => {
  return `${secondName} & ${thirdName}`
}printName(names);//Returns ---> 'Luke & Ben'
```

上面的例子首先创建了一个名为 *names* 的数组，其中包含了名称字符串。我们创建了一个名为 *printName* 的函数，它使用模板文本从 names 数组中返回第二个和第三个名字。在函数的括号内，我们首先使用逗号，因为我们想跳到第二个数组元素，接下来我们声明第二个和第三个元素的变量，以存储在， *secondName* 和 *thirdName* 中。当调用 *printName* 函数时，我们传入整个 *names* 数组。

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****