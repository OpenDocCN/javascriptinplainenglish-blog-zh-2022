# 单元测试最简单的例子:纯函数

> 原文：<https://javascript.plainenglish.io/the-simplest-case-for-unit-tests-pure-functions-d80a583dbe0f?source=collection_archive---------15----------------------->

## 纯函数是单元测试中最简单的。

![](img/ebc5b3cb35400f42f83fcf4c8c1c516c.png)

Illustration by the author

整个行业的开发团队都在使用单元测试来维护他们代码的质量。然而，似乎许多面向初学者的材料并没有真正涵盖单元测试。这很不幸——添加单元测试是我喜欢交给团队新同事的一项完美的入职任务。通过习惯单元测试，他们可以开始熟悉代码库并取得显著的进步，同时不会面临与构建面向客户的更改相关的风险或压力。

# 什么是单元测试

单元测试是根据明确的预期来验证代码单元的小段代码。您编写它们是为了给自己一种自动检查代码的方法。因此，当您继续处理代码库时，可以快速检查事情是否按预期运行。

在现实世界的 JavaScript 项目中，人们通常使用这些开源框架之一进行测试:

*   茉莉
*   玩笑
*   摩卡

在本文中，为了简单起见，我将使用受这些框架启发的伪代码。

# 什么是纯函数？

纯函数是其结果仅取决于所提供的参数的函数。它们不保持内部状态，也不读取除参数之外的外部值。它们在数学意义上与函数相同。例如:

*   `sin(x)`，
*   `cos(x)`，
*   `f(x) = 4 * x + 5`。

# 数据操作

让我们定义一个问候函数:

```
function greet(name, surname) {
  return `Hello ${name} ${surname}!`;
}
```

这是一个纯函数:每次当我运行`greet('Marcin', 'Wosinek')`时，它都会返回‘Hello Marcin Wosinek！’。

# 测试一下！

如何测试这个功能？

```
expect(greet('Lorem', 'Ipsum')).toEqual('Hello Lorem Ipsum!');
```

测试框架将上面的代码变成类似于:

```
if(greet(‘Lorem’, ‘Ipsum’) !== ‘Hello Lorem Ipsum!’) {
  throw new Error(“greet(‘Lorem’, ‘Ipsum’) doesn’t equal ‘Hello Lorem Ipsum!’”)
}
```

并向您显示他们运行的所有检查的结果报告。

# 边缘案例

编写单元测试让你思考边缘案例。例如，如果我们的函数只有一个参数被调用，那么会发生什么*？称呼对方的名字听起来是最合理的事情，但是当前的实现做了不同的事情:*

```
greet(‘Marcin’); // returns “Hello Marcin undefined!”
```

如果我们想做仅支持名字的调用，我们可以添加下面的测试用例:

```
expect(greet(‘Lorem’)).toEqual(‘Hello Lorem!’);
```

这将需要改进我们的实施:

```
function greet(name, surname) {
  if (surname) {
    return `Hello ${name} ${surname}!`;
  } else {
    return `Hello ${name}!`;
  }
}
```

类似地，我们可以继续添加其他边缘案例。例如，应该发生什么:

*   当我们问候只有姓氏的人时
*   没有名字或姓氏
*   当用三个参数调用该方法时——用中间名或第二个姓

通过考虑这些情况并为它们添加测试，我们可以构建更具弹性的代码。

# 折扣计算

让我们用钱来尝试一些操作。假设我们正在构建一个商店系统，我们想要一个对价格应用折扣的方法。一个快速而肮脏的解决方法是:

```
function calculateDiscountedPrice(originalPrice, discount) {
  return originalPrice - originalPrice * discount;
};
```

# 测试一下！

让我们考虑几个可以测试的案例:

```
// case 1
expect(calculateDiscountedPrice(10, 1/4)).toBe(7.5);

// case 2
calculateDiscountedPrice(0.9, 2/3).toBe(0.3)

// case 3
expect(calculateDiscountedPrice(10, 1/3)).toBe(6.67);
expect(calculateDiscountedPrice(10, 2/3)).toBe(3.33);
```

这些例子看起来有点重复吗？实际上，它们是非常不同的，只有*案例 1* 在我们当前的实现中会像预期的那样工作。

# 边缘案例

在我们的边缘案例中会发生什么？在*案例 2* 中，我们遇到了由数字在 JavaScript 中的存储方式引起的舍入误差。JavaScript 只有*浮点*数字，所以每一个舍入小数在内存中用一个近似值表示，这个近似值会引入一个微小的舍入误差。当您对数字进行运算时，这些错误会累积起来，最终得到的结果会与您的预期略有出入。在我们的案例中:

```
calculateDiscountedPrice(0.9, 2/3)
0.30000000000000004
```

和`0.3`很接近，但不是同一个值。对于我们处理货币的应用程序来说，以一种清除这些错误的方式实现货币操作是有意义的。

*情况 3* 测试将因缺少舍入而失败——函数返回`6.666666666666667`和`3.333333333333334`。在大多数系统中，我们只关心精确到小数点后第二位的值——精确到分。

这两个问题都可以通过相同的实现调整来解决:

```
function calculateDiscountedPrice(originalPrice, discount) {
  const newPrice = originalPrice - originalPrice * discount;
  return Math.round(newPrice * 100) / 100
};
```

它总是按预期工作吗？不一定——你可以查看这个[堆栈溢出线程](https://stackoverflow.com/questions/11832914/how-to-round-to-at-most-2-decimal-places-if-necessary)来了解边缘情况。如果可能的话，您可能希望使用一些第三方库来为您进行舍入。

# 数学运算

让我们考虑一些纯数学运算:

```
function power(base, exponent) {
  return base ** exponent;
};
```

这里有什么我们可以测试的有趣的东西吗？

# 测试一下！

```
// case 1
expect(power(2, 2)).toBe(4);
expect(power(2, 10)).toBe(1024);
expect(power(2, 0)).toBe(1);

// case 2
expect(power(0, 0)).toBe(NaN);
```

*案例 1* 按预期工作，而*案例 2* 失败:JS 返回 1，这和我们在数学里学的不一样。

# 边缘案例

我们还能在这里测试什么？我们可以扩展我们的测试，覆盖不正确参数的情况，例如:

*   `power()`，
*   `power(‘lorem’, ‘ipsum’)`，
*   `power({}, 0)`。

为什么要测试那些案例？因为它们可能发生在应用程序中，你的程序会对它们做些什么。如果您花一些时间思考在您的应用程序环境中什么是最有意义的，您会更好:

*   返回`NaN`，
*   抛出错误，或者
*   默认为某个合理的值，例如`1`

无论您做出什么决定，您都可以在单元测试中将其明确化。

# 想了解更多？

我在博客上写了更多关于单元测试的内容:

*   [如何编写单元测试](https://how-to.dev/how-to-write-unit-tests)，
*   单元测试有什么意义？

# 摘要

纯函数是单元测试中最简单的。尽管如此，写它们会让你有正确的心态去发现边缘案例，否则就不会被正确地考虑。对于初学编程的人来说，这是一项有价值的练习和技能:它教会你以一种非常精确的、类似机器的方式思考；提高单元测试覆盖率对许多项目来说是一个受欢迎的贡献。

*最初发布于*[*https://how-to . dev*](https://how-to.dev/the-simplest-case-for-unit-tests-pure-functions)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ，*和* [***不和***](https://discord.gg/GtDtUAvyhW) *。***