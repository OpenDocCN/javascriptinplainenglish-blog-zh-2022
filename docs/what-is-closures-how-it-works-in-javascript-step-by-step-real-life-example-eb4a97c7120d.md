# 什么是闭包&它在 JavaScript 中是如何工作的？

> 原文：<https://javascript.plainenglish.io/what-is-closures-how-it-works-in-javascript-step-by-step-real-life-example-eb4a97c7120d?source=collection_archive---------1----------------------->

## 带有真实例子的 JavaScript 闭包教程。

![](img/116779ae495b67bd8e5aa363f5650621.png)

一个**闭包**是一个捆绑在一起(封闭)的函数的组合，并引用其周围的状态，让**简化这个定义**。

我将用下面的真实用例来说明闭包:

*让我们假设我们想要创建一个变量，我们称它为* `*counter*` *，并将其初始化为 0，然后我们将在每次函数调用后给它加+1，然后，我们将在 3 次函数调用后将结果打印到控制台。我们期待收到数字 3。*

让我们看看下面的解决方案示例:

```
var counter = 0;function plusOne(){
  counter = counter + 1;
  return counter;
}plusOne();
plusOne();
plusOne();console.log(counter); // Will print 3.
```

## 这个解决方案有什么问题？

问题是每个人都可以改变那个`counter`变量，而这对我们没有好处，我们希望只有函数`plusOne()`将可以做到这一点。

## 那么我们需要做什么呢？

为了保证只有函数`plusOne()`可以修改`counter`变量，我们必须将`counter`变量设置为`plusOne()`函数范围的局部变量。

```
function plusOne(){
  var counter = 0;
  counter = counter + 1; return counter;
}plusOne();
plusOne();console.log(plusOne()); // Will print 1.
```

## 这个解决方案有什么问题？

现在我们有了`plusOne()`函数的局部变量`counter`，**太好了！**，但这还没完，我们对`plusOne()`函数的 3 次函数调用后，永远不会收到数字 3，因为我们在每次函数调用后，都将局部变量`counter`重新定义为 0。

## 那么我们需要做什么呢？

我们需要在`plusOne()`函数中有一个内部函数，它可以访问`counter`变量，允许我们修改它。

```
function plusOne(){
  var counter = 0;
  function add(){
    counter = counter + 1;
  }
  add() //Call to the add() function to add 1 to counter. return counter;
}plusOne();
plusOne();console.log(plusOne()); // Will print 1.
```

## 这个解决方案有什么问题？

这个解决方案仍然会将 1 而不是 3 打印到控制台，但是我们已经非常接近最终的解决方案了。那么，这个解决方案有什么问题呢？请注意，我们仍然为每个调用重新定义了`counter`变量。如果我们可以只访问内部函数`add()`而不去重定义代码，这个问题就解决了。

# 最终解决方案

```
const plusOne = (function add(){
  var counter = 0; return function {
    counter = counter + 1;
    return counter;
  }
})();plusOne();
plusOne();console.log(plusOne()); // Will print 3.
```

所以现在我们将打印 3 作为`counter`值，但是这里实际发生了什么呢？

首先，我们声明`plusOne`变量是一个变量而不是一个函数，然后内部函数`add()`现在包含了`counter`变量，但是除此之外，它还返回一个函数给`plusOne`变量，使`pluseOne`变量成为一个函数，但是这里最重要的部分是返回给`plusOne`变量的函数包含了父作用域，所以每次我们调用`plusOne`函数(它是变量并变成了函数)时，返回的函数会记住计数器`variable`的最后一个值。

这被称为 JavaScript **闭包。**它使得函数有可能拥有“**私有**变量。

这样我们保证只有`plusOne()`函数可以访问和修改`counter`变量，并且不会使`counter`变量处于**全局作用域**中。

**感谢您迄今为止的阅读，**如果您喜欢这样的内容，并且您想支持我作为一名程序员和作家撰写更多这样的文章， [***请使用我的链接注册 Medium 成为会员(每月订阅 5 美元)，您将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

如果你想了解更多关于作用域和每个作用域之间的区别，你可以在这里阅读:

[](https://nissimzarur.medium.com/4-types-of-javascript-scopes-all-you-need-to-know-about-207598da120e) [## 4 种类型的 JavaScript 作用域——您需要了解的全部内容

### 我看到许多前端开发人员不确定什么是作用域，即使他们每天在工作中使用它。我决定…

nissimzarur.medium.com](https://nissimzarur.medium.com/4-types-of-javascript-scopes-all-you-need-to-know-about-207598da120e) 

谢谢，希望对你有帮助。关注我，了解更多 JavaScript 解释、示例和技巧。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*