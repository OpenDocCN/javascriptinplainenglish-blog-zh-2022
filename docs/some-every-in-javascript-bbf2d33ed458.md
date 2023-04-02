# 如何在 JavaScript 中使用 some() & every()

> 原文：<https://javascript.plainenglish.io/some-every-in-javascript-bbf2d33ed458?source=collection_archive---------14----------------------->

## 关于如何在 JavaScript 中使用数组助手方法 some() & every()的教程

![](img/a6296fa544de698e2bf0bc449fc01908.png)

**some()** 和 **every()** 数组方法是 ES6 中引入的两个数组助手方法。这两种方法都返回布尔值(真或假)。我们将从查看每个。

## **一举()**

当我们使用 every()时，我们传入一个回调方法(通常是一个匿名函数)。回调方法需要返回一个布尔值，我们可以把这看作是一个测试方法。该方法将针对数组中调用 every()的每个元素运行一次。如果所有元素都通过了测试回调方法，将返回 true。如果一个或多个元素没有通过测试回调方法，将返回 false。让我们看一个基本的例子:

```
const names = ["Abby", "Anna", "Alice"];names.every(function(name) {
  return name.includes("A");
});//Returns ---> true
```

在上面的例子中，我们使用 const 声明了一个名为*的变量。我们给它分配一个包含三个字符串的数组。然后我们在 *names* 数组上使用 *every()* ，传入回调，并设置一个 *name* 参数。 *name* 参数将代表 *names* 数组中的每个元素。我们返回 *name* 元素是否包含字母 *A* 。 *names* 数组中的所有元素都包含字母 *A* ，因此返回 true。*

因为我们正在使用 ES6，所以让我们将函数更新为使用箭头函数。

```
const names = ["Abby", "Anna", "Alice"];names.every(name => name.includes("A"));//Returns ---> true
```

我们还可以将调用 every()的结果存储到一个变量中，这样我们就可以在其他时候访问它。

```
const names = ["Abby", "Anna", "Alice"];const includesA = names.every(name => name.includes("A"));
console.log(includesA);//Returns ---> true
```

如果我们的 *names* 数组中有任何不包含字母 *A* 的元素，我们将得到 false 返回。这是因为只需要一个元素没有通过测试函数，所有元素都没有通过。我们将把名字 *Bob* 添加到 *names* 数组中，然后再试一次。我们得到 false 返回，如下例所示:

```
const names = ["Abby", "Anna", "Alice", "Bob"];const includesA = names.every(name => name.includes("A"));
console.log(includesA);//Returns ---> false
```

## 嵌套数据结构

如果我们使用嵌套的数据结构，every()方法对于评估我们的某些数据非常有帮助。如果我们有一个学生测试结果的列表，并且我们想知道是否所有的学生都通过了测试，我们可以使用 every()。

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
    score: 80
  },
];const didPass = results.every(student => student.score > 50);
console.log(didPass);//Returns true
```

在上面的例子中，我们声明了一个名为*结果*的变量。我们给它分配一个包含三个对象的数组。这些对象包含学生的*姓名*和*分数*。然后我们声明另一个名为*的变量 didPass* 。我们将在我们的*结果*数组上调用 *every()* 的结果赋给它。我们设置一个*学生*参数，并检查该学生的*分数*是否大于 50。我们的*结果*对象数组中的所有学生得分都高于 50，因此我们返回了 true。

## 一些()

当我们使用 *some()* 时，我们传入一个回调方法(通常是匿名函数)。回调方法需要返回一个布尔值。与 *every()，*一样，我们可以把这看作一种测试方法。该方法将对数组中调用 some()的每个元素运行一次。如果任何元素通过测试回调方法，将返回 true。如果没有一个元素通过测试，回调方法将返回 false。

## 一些()与每个()

澄清一下*如果有任何元素通过测试函数，some()* 将返回 true，而 e *very()* 仅当所有元素都通过测试函数时才返回 true。如果你不是在寻找通过测试函数的所有东西，只是一个元素，那么 *some()* 是一个有用的方法。让我们来看一些()的基本例子。

```
const ages = [1, 2, 10, 1];const higherThanFive = ages.some(age => age > 5);
console.log(higherThanFive);//Returns ---> true
```

在上面的例子中，我们声明了一个名为*的变量 ages* 。我们给它分配一个包含四个数字的数组。然后，我们声明一个名为 *higherThanFive* 的变量，并将对 *ages* 数组使用 some()方法的结果赋给这个变量。我们传递回调并设置一个*年龄*参数。我们检查是否有一个*年龄*元素大于 5。来自 *ages* 数组的一个元素大于 5，所以我们得到 true 返回。

如果我们将 *ages* 数组改为只包含小于 5 的数字，我们将得到 false。这是因为 *ages* 数组中没有任何东西通过测试函数。下面是一个例子:

```
const ages = [1, 2, 3, 1];const higherThanFive = ages.some(age => age > 5);
console.log(higherThanFive);//Returns ---> false
```

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*