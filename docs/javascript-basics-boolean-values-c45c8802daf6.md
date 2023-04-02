# JavaScript 基础:布尔值

> 原文：<https://javascript.plainenglish.io/javascript-basics-boolean-values-c45c8802daf6?source=collection_archive---------24----------------------->

## 对还是错

![](img/d65e90544a1332d054f2b37186cf9a1a.png)

Photo by [Jeremy Bezanger](https://unsplash.com/@unarchive?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，有一种方法可以打开或关闭值，或者将值设置为是或否，而不需要使用字符串来确定。这就是布尔类型出现的时候。在 JavaScript 中，布尔类型不是`true`就是`false`。

以下是布尔输出的一个示例:

```
console.log(4 > 5) // false
console.log(12 < 43) // true
```

使用小于`<`操作符和大于`>`操作符，JavaScript 将输出 true 或 false。

当使用类似的运算符如大于或等于`>=`、小于或等于`<=`、等于`==`和不等于`!=`时也是如此。

```
console.log("noun" == "crown") // false
console.log("Far" != "park") // true
```

当在字符串上使用大于或小于运算符时，JavaScript 将比较每个字符的 Unicode 值。在 Unicode 中，字母按字母顺序排列，但区别在于大写字符小于小写字符，小写字符小于非字母字符。

`NaN` or not 数字是 JavaScript 中唯一不等于自身的值。废话连篇的计算不能真正等同于其他废话连篇的计算。

上面的例子是比较运算符。还可以使用逻辑运算符输出布尔值。

有三个逻辑运算符:*与*、*或*、*非。*

如果比较的两个值都为真，and 运算符或`&&`将输出真。

```
console.log(true && true) // true
console.log(false && true) // false
```

如果其中一个比较值为真，or 运算符或`||`将输出真。

```
console.log(true || false) // true
console.log(false || false) // false
```

not 运算符或`!`将翻转赋予它的值。所有真值变为假，所有假值变为真。

```
console.log(!false) // true
console.log(!true) // false
```

你可以把这些布尔运算符和算术混合起来，就像算术一样，先比较什么是有顺序的。or 运算符优先级最低，然后是 and 运算符，最后是比较运算符。其他的都是后来才出现的(数学运算符，数字等等)。

```
3 + 4 == 7 && 7 + 0 == 7
```

您可以用括号将这些值括起来。括号内的项目优先级最高。

```
(5 + 13 > 45) || (12 / 3 == 4)
```

还要提到的一个逻辑运算符是三元运算符。它就像是对`if…else`语句的替代。

这里有一个例子:

```
let beverage = (age >= 21) ? "Beer" : "Juice";
```

上面的语句相当于写:

```
if (age >= 21){
    beverage = "Beer";
}else{
    beverage = "Juice";
}
```

如果问号前的语句为真，它将把`"Bear"`赋给`beverage`变量，否则，它将把`"Juice"`赋给变量。

你可以在这里阅读更多关于[三元运算符的内容。](https://levelup.gitconnected.com/javascript-basics-ternary-operator-c5e1510c6d2)

如果你想阅读更多的 JavaScript 基础文章，你可以看看我最近的文章:

[](/javascript-basics-numbers-352d49a61335) [## JavaScript 基础:数字

### JavaScript 中的数字

javascript.plainenglish.io](/javascript-basics-numbers-352d49a61335) [](https://levelup.gitconnected.com/javascript-basics-strings-a275d1e4b573) [## JavaScript 基础:字符串

### JavaScript 中的字符串

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-basics-strings-a275d1e4b573) [](https://codeburst.io/javascript-basics-default-parameters-and-return-statements-e5f2f07daf6a) [## JavaScript 基础知识:默认参数和返回语句

### 在我们上一篇 JavaScript 基础文章中，我们讨论了如何使用 JavaScript 函数。

codeburst.io](https://codeburst.io/javascript-basics-default-parameters-and-return-statements-e5f2f07daf6a) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***