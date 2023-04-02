# JavaScript 面试问题:JavaScript 解构(ES 6)

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-javascript-destructuring-es-6-df197d729632?source=collection_archive---------10----------------------->

## 关于如何在 JavaScript 中使用**析构**的教程，并附有示例。

![](img/b99e5d9a04e33045837ea59a10fd050d.png)

# JavaScript 面试问题# 6

**JavaScript** 和**中的**析构** **是什么我们如何使用析构**？**

大家好，在本教程中我们将通过例子学习如何在 JavaScript 中使用**析构**。

在 JavaScript 的 **ES6** 的帮助下，我们可以开始使用析构了。这使得从数组和对象中创建新变量变得更加容易。

## 我们如何对对象使用析构

让我们看看如何在 JavaScript 中对对象使用析构。

让我们首先创建我们的对象作为例子

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
  "hair_color": "n/a",
  "skin_color": "white, blue",
  "eye_color": "red",
  "birth_year": "33BBY",
  "gender": "n/a",
}
```

我们已经创建了我们的 **r2d2** 变量。我们如何通过对象析构来访问那个变量的 **name** 属性呢？

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
  "hair_color": "n/a",
  "skin_color": "white, blue",
  "eye_color": "red",
  "birth_year": "33BBY",
  "gender": "n/a",
}**const { name } = r2d2; 
console.log(name)
// R2-D2**
```

正如你在上面的例子中看到的，我们创建了一个新变量`name`并赋予了 **r2d2 name 属性。**

如果我们想访问对象内部的多个属性，我们可以这样做:

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
  "hair_color": "n/a",
  "skin_color": "white, blue",
  "eye_color": "red",
  "birth_year": "33BBY",
  "gender": "n/a",
}**const { name, height, mass } = r2d2; 
console.log(name)
// R2-D2
console.log(height)
// 96
console.log(mass)
// 32**
```

我们已经用 r2d2 变量的属性创建了`name`、`height`和`mass`变量。

## 在 ES6 之前，我们如何访问对象属性？

如果我们想在 ES6 之前访问对象属性，我们应该这样做:

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
  "hair_color": "n/a",
  "skin_color": "white, blue",
  "eye_color": "red",
  "birth_year": "33BBY",
  "gender": "n/a",
}const name = r2d2.name;
const height = r2d2.height;
const mass = r2d2.mass;console.log(name)
// R2-D2
console.log(height)
// 96
console.log(mass)
// 32
```

如你所见，我们必须从对象中创建所有带点符号的变量，这意味着我们必须编写更多的代码行:)

## 我们如何在析构时分配对象键

还有一个非常重要的特性，我们可以用来在析构的时候给不同的变量名赋值。

如果您已经在作用域中定义了相同的变量名，它将允许您使用另一个变量名，而无需覆盖现有的变量名。

下面是我们如何做到这一点的一个例子:

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
  "hair_color": "n/a",
  "skin_color": "white, blue",
  "eye_color": "red",
  "birth_year": "33BBY",
  "gender": "n/a",
}**const { name:robotName, height:robotHeight, mass:robotMass } = r2d2;****console.log(robotName)
// R2-D2
console.log(robotHeight)
// 96
console.log(robotMass)
// 32**
```

正如你在这里看到的，我们分配了:
- **名称**到**机器人名称**
- **高度**到**机器人高度**
- **质量**到**机器人质量**

```
**const { name:robotName, height:robotHeight, mass:robotMass } = r2d2;**
```

## 数组中的析构

在数组中使用析构也是我们将要讨论的一个非常重要的主题。

让我们看一个使用数组析构的例子。

```
const arrayValues = ['luke skywalker', '3cpo', 'r2d2'];

// destructuring in arrays
const [x, y, z] = arrayValues;

console.log(x); // luke skywalker
console.log(y); // 3cpo
console.log(z); // r2d2
```

正如你在例子中看到的，我们已经创建了 3 个不同的变量，命名为 **x，y，z
这些值也分配如下:**

```
x = "luke skywalker"
y = "3cpo"
z = "r2d2"
```

## 分配默认值

使用析构时，默认值可以在析构过程中赋值。

**在数组中分配默认值**

```
let arrayValue = [13];

// assigning default value 5 and 7
let [x = 5,  y = 7, z = 10] = arrayValue;

console.log(x); // 13 (Only first value exists in array)
console.log(y); // 7
console.log(z); // 10
```

在上面的例子中**只有第一个值存在于数组中**，并且**没有使用 x 的默认值，而是将 13 传递给了 x。**

**在对象中分配默认值**

我们也可以对析构的对象做同样的事情。

```
const robot = {
    name: 'r2d2',
}// assign default value 100 to height if undefined
const { name, height = 100} = robot;console.log(name); // r2d2
console.log(height); // 100
```

## 如何在数组析构中跳过元素

当数组中使用了析构时，这些值需要按顺序排列。如果我们想跳过数组中的一些值呢？

让我们看看下面的例子:

```
let arrayValue = [3,5,7];

// assigning default value 5 and 7
let [x, ,z] = arrayValue;

console.log(x); // 3
console.log(z); // 7
```

正如你看到的，我们在析构的时候没有使用第二个值，所以我们只从**数组值**中创建了 **2 个变量**作为 **x** 和 **z**

## 将剩余值析构为单个变量

当在 javascript 数组或对象中进行析构时，我们可以**选择变量**并将剩余的变量**分配给一个变量**

为了做到这一点，我们需要在变量赋值之前使用`...`(展开语法)**。**

让我们来看看下面这个用 spread 运算符进行数组析构的例子:

```
const arrayValue = [1, 2, 3, 4];

// assigning remaining elements to y with three dots
const [x, ...y] = arrayValue;

console.log(x); // 1
console.log(y); // [2, 3, 4] const [k,l ...m] = arrayValue;
console.log(k); // 1
console.log(l); // 2
console.log(m); // 3,4
```

在第一个示例中，我们将第一个值**分配给 x** 并将剩余值**分配给 y.** 在第二个示例中，我们将 k 分配给 1，l 分配给 2，剩余值分配给 m.

让我们看看如何对对象使用 spread 语法，如下所示:

```
const r2d2 = {
  "name": "R2-D2",
  "height": "96",
  "mass": "32",
}const { name, ...anotherValues } = r2d2;console.log(name) // R2-D2
console.log(anotherValues) // {height: "96", mass: "32"}
```

将**命名变量**和**剩余**的值赋给**另一个值**变量

如果你想了解更多关于**扩展操作符**的信息，你可以阅读我的另一篇文章:

[](https://melih193.medium.com/javascript-interview-questions-javascript-spread-operator-es-6-98f24f420bf0) [## Javascript 面试问题:Javascript Spread 运算符(ES 6)

### Javascript 面试问题# 7——Javascript 中的 spread 操作符是什么，我们如何使用 spread 操作符？

melih193.medium.com](https://melih193.medium.com/javascript-interview-questions-javascript-spread-operator-es-6-98f24f420bf0) 

这就是关于 JavaScript 析构的全部内容:)

看完这篇文章，希望你能回答所有 **JavaScript 析构面试问题**。

*如果你觉得这篇文章很有帮助，你可以通过使用我的推荐链接注册一个* [***中级会员来访问类似的***](https://melihyumak.medium.com/membership) *。*T54

***跟我上*** [**推特**](https://twitter.com/hadnazzar)

[![](img/c012fae801a3ab846a63dc560d09ff17.png)](https://www.youtube.com/c/TechnologyandSoftware)

Subscribe for more on [**Youtube**](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)

# 编码快乐！

梅利赫

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*