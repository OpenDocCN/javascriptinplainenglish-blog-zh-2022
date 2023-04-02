# 成为一名 JavaScript 忍者:学习 currying 的魔力

> 原文：<https://javascript.plainenglish.io/become-a-javascript-ninja-learn-the-magic-of-currying-5630028e4860?source=collection_archive---------15----------------------->

![](img/707970bd9da1b8b1acdf9b6c7098901b.png)

[https://unsplash.com/photos/xrVDYZRGdw4](https://unsplash.com/photos/xrVDYZRGdw4)

## 关于 JavaScript 中的 Currying 函数，您需要知道的一切:示例和最佳实践

currying 函数是一种允许将需要多个参数的函数转换成一系列只需要一个参数的函数的技术。例如，考虑以下函数:

```
function sum(a, b) {
  return a + b;
}
```

我们可以使用“curry”函数将其转换为 curry 函数，如下所示:

```
function curry(fn) {
  return function(x) {
    return function(y) {
      return fn(x, y);
    }
  }
}

// usage
function sum(a, b) {
  return a + b;
}

const curriedAdd = curry(sum);
```

现在，我们可以使用“curriedAdd”函数来代替原来的“Add”函数。但是，我们必须一次传递一个参数，如下所示:

```
const addFive = curriedAdd(5);
const result = addFive(10);

console.log(result); //15
```

在本例中，我们创建了一个名为“addFive”的新函数，该函数为作为参数传递的任何值加 5。然后，当我们调用“addFive(10)”时，结果将是 15。

currying 函数一开始可能有点难以理解，但是一旦掌握了它的窍门，它就可以成为编写更简洁、更灵活的代码的非常强大的工具。此外，当使用使用 currying 函数提供高级功能的第三方库时，它可能特别有用。如果你想成为一名真正的 JavaScript 忍者，学习 currying 的魔力是重要的一步！

举个简单的例子，currying 类似于 matryoshkas，每个函数都可以比作一个玩偶。每次你调用一个函数，就好像你打开了一个洋娃娃，你把它放在一张桌子上，写下你传递给它的参数。一旦你调用了所有的函数或者打开了所有的玩偶，你就可以用所有的参数进行操作了。

如您所见，currying 的实现很简单:它涉及两层函数。

1.  最外层的函数名为“curry”，它以一个正则函数作为参数(如“sum”)并返回一个新函数(姑且称之为“wrapperA”)。
2.  当使用第一个参数(例如“1”)调用“wrapperA”时，保存该值并返回一个新函数(姑且称之为“wrapperB”)。
3.  然后，当用第二个参数(例如“2”)调用“wrapperB”时，它用保存的值和新的参数调用原始的“sum”函数。

currying 的一个用例是当您想要创建一个现有函数的专用版本时。例如，假设您有一个计算订单总成本(含税)的函数。您可以使用 currying 创建该函数的一个专门版本，该版本只设置税，如下所示:

```
function calculateCost(tax, price) {
  return tax + price;
}

const setTax = curry(calculateCost);
```

现在，您可以使用“setTax”函数快速方便地设置任何价格的税，而不必指定其他参数。这可以使代码更具可读性和可维护性:您可以只添加固定税收的价格。

```
// onlyPrice will be the partial of cost with fixed first argument
let onlyPrice = setTax(5);

// use it passing only the price
var productOne = onlyPrice(10); 
console.log(productOne); // 15 (tax + price)

var productTwo = onlyPrice(30); 
console.log(productTwo); // 35 (tax + price)

var productThree = onlyPrice(50); 
console.log(productThree); // 55 (tax + price)
```

## 高级形式

## 结论

一般来说，使用 currying 可以使你的代码更加灵活和可重用。不必为每个参数组合编写单独的函数，您可以编写一个函数，并根据需要使用 currying 创建该函数的专用版本。这可以节省您的时间，并使您的代码更有组织性和效率。所以，如果你想成为一名真正的 JavaScript 高手，学习 currying 的艺术是必须的！

在推特或 T2【LinkedIn】上关注我，了解其他建议！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*