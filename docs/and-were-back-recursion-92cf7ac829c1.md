# 什么是递归？

> 原文：<https://javascript.plainenglish.io/and-were-back-recursion-92cf7ac829c1?source=collection_archive---------16----------------------->

## 关于递归你需要知道的一切。

![](img/4021b1bd49569c75fa7094f96f7b2db5.png)

Photo by [Mario Mesaglio](https://unsplash.com/@seimesa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/recursivity?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

嘿，伙计们，愿每个人都拥有精神、身体和灵魂的力量。在过去的几个星期里，我一头扎进了递归，不可否认的是，最初我并不喜欢它，但是在花了一些时间并完成了一些练习之后，我开始欣赏这种方法，因为在某些情况下，它证明了比迭代更好的方法。但是什么是递归呢？

简单地说，递归是一个不断重复的过程，直到满足某种条件。在 CS 方面，这个过程是由一个函数提供的。所以一个递归函数会反复调用自己，直到到达某个边界，然后返回，停止执行。这个*边缘情况*通常被称为**基础情况**和作为递归函数的停止点。

这一点很重要，因为与压入调用堆栈并在完成执行后弹出的普通函数调用不同，递归函数不断地将函数压入调用堆栈。因此，如果没有提供基本情况，函数将永远执行自己，这可能导致浏览器抛出一个错误**“超出最大调用堆栈大小】，**意味着堆栈已经因重复的函数调用而过载。这也称为**堆栈溢出。**

除了基本情况，递归函数还需要调用自身，但是使用不同的输入，这导致了一些基本情况。这确保了会有一个停止点。这将更有意义，因为我举例说明了字符串反转练习的递归解决方案。但是首先我想给那些不熟悉或者对 JavaScript 调用栈以及同样重要的*栈*数据结构了解有限的人一些背景知识。

## JavaScript 的调用堆栈

调用栈(高层)是 JavaScript 引擎的一个组件，它管理程序中的函数调用——它检查当前正在运行什么函数，以及从该函数内部调用了什么函数(如果有)。当一个函数被调用时，它被*推入*堆栈，一旦该函数执行完毕，它就被*弹出*堆栈。

## 堆栈

更具体地说，*堆栈*是一种线性数据结构，其中数据元素按顺序组合在一起——因此函数调用按调用顺序放入堆栈。堆栈遵循**后进先出(LIFO)** 原则，这意味着最后一个被推入堆栈的元素将首先弹出。一个臭名昭著的类比指向一堆互相堆叠的盘子*。每个板块代表一个函数调用。最上面的盘子将最先脱落，因为它是最后添加的。类似地，当函数完成执行时，推入调用堆栈的最后一个函数调用是第一个弹出的。*

有了这个心理模型，让我们使用递归方法来完成*字符串反转*练习。本练习摘自柯尔特·斯蒂尔的 [*JS 算法& DS 教程*](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass/) 。

```
Write a recursive function called ***reverse***which accepts a string and returns a new string in reverse.
```

```
function reverse(str){
 let reversedWord = "";
  if (str.length <= 0) {
    return "";
  }const helper = function (strInput) {
    reversedWord = reversedWord.concat(
      strInput[strInput.length - 1],
      reverse(strInput.slice(0, -1))
    );
  }; helper(str);
  return reversedWord;
}
```

以上是我在潜意识中尝试形成解决方案几个小时后想出来的一个解决方案。从第一行开始，需要返回一个反转的字符串，所以我们初始化一个空字符串 ***reversedWord。*** 移动到下一行是我们的条件，将停止函数递归执行。在这种情况下，如果传入的字符串长度过时，我们将返回一个空字符串。

```
const helper = function (strInput) {
    reversedWord = reversedWord.concat(
      strInput[strInput.length - 1],
      reverse(strInput.slice(0, -1))
    );
  };
```

这就是我们达到函数递归性质的地方。我们创建一个 ***助手*** 函数，其唯一目的是操纵 ***反转字*** 字符串。它将传入的字符串的最后一个字母和下一个 *reverse* 函数调用的最后一个字母连接起来，直到传入的字符串为空。所以对于每个函数调用，我们都在处理传入的原始字符串的一个更小的子集，直到我们满足基本情况，是一个空字符串。

```
"lmth" ---> "html"
1st call – reversedWord("tml") returns "h" --> concat("h", "tml")
2nd call – reversedWord("ml") returns "t" --> concat("t", "ml")
3rd call – reversedWord("l") returns "m" --> concat("m", "l")
4th call – reversedWord("") returns "l" --> concat("l", "")
5th call - returns "" --> strings length is 0
```

这是用传入的字符串调用的*助手*函数的可视化模型。如图所示，最后一个 ***反向*** 调用根据我们的基本情况返回一个空字符串。从这一点开始，我们向后移动到第一个 ***反向*** 调用。

从返回一个空字符串开始，我们将这个空字符串连接到前一个函数的当前字母`'l'`。一旦完成，函数*从堆栈中弹出*并调用该函数，这次使用原始字符串的一个较小的子集。因此，对于我们的字符串`'l'`，我们执行同样的事情，并将它与前一个函数的当前字母`m`连接起来，因此`reversedWord.concat('m', 'l')`将导致`'ml’`——直到我们得到一个完全反转的字符串。如果您注意到，每个递归调用都等待下一个返回一个*字符串*，这样它就可以将自己的字符串连接到它上面，最终得到一个反转的单词。

现在很快，我想分享一个使用*纯递归*的替代解决方案。我最初的解决方案是使用*助手方法递归*实现的，使用嵌套函数来操作 *reversedWord* 字符串并在最后返回它。使用纯递归，函数本身是独立的，这意味着它不会对任何外部代码产生任何副作用。我计划在以后的文章中更深入地讨论这两种方法。但是现在，我想实现一个解决方案，使用这两种方法来巩固每一种方法。以下是解决方案:

```
const reverse = function (string) { let reversedStr = ""; if (string.length <= 0) { return ""; } return reversedStr.concat( string[string.length - 1], reverse(string.slice(0, -1)) );};
```

*本文到此结束，感谢您花时间阅读本文。虽然有点冗长，但我希望你们能学到一两件事。一如既往，我渴望听到关于如何改进我的代码解决方案或写作的建议。如果你想陪伴我成为一名前端开发人员，请关注**my*[*Twitter*](https://twitter.com/thedetroitdev)*和*[*LinkedIn*](https://www.linkedin.com/in/erick-walker-0433981ab/)*。愿和平与祝福带给每一个人。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*