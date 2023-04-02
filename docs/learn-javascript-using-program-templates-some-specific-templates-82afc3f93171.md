# 使用程序模板学习 JavaScript:一些特定的模板

> 原文：<https://javascript.plainenglish.io/learn-javascript-using-program-templates-some-specific-templates-82afc3f93171?source=collection_archive---------21----------------------->

## 第 1 部分:在非常特殊的情况下使用的程序模板。

![](img/fba654aa9a47e4fde507d77ab8e6e5cc.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本系列过去关于使用程序模板学习 JavaScript 的文章中，我一直关注可以用于许多不同问题的通用模板。在这篇文章中，我想集中讨论一些在非常特殊的情况下使用的程序模板。我将从*变量交换*模板开始，然后是*提取数字*模板，最后是*寻找三个值的最小值*模板。

# 变量交换程序模板

当你收集数据时，你必须做的一件事就是把它整理成某种类型的顺序。根据数据类型，顺序可以是数字或字母。当你对数据进行排序时，变量值经常需要被交换以得到正确的顺序。可以使用程序模板*变量交换*模板来交换变量值。

以下是该模板的伪代码:

*变量是 val1 和 val2
将 val1 的值赋给一个临时变量。
将 val2 的值赋给 val1。
将临时变量的值赋给 val2。*

让我们使用下面的程序来看看这在实践中是如何工作的:

```
let var1 = 23;
let var2 = 12;
print(var1, var2);
let temp = var1;
var1 = var2;
var2 = temp;
print(var1, var2);
```

这个程序的输出是:

```
23 12
12 23
```

我们可以用绳子做同样的事情:

```
let word1 = "apple";
let word2 = "aardvark";
print(word1, word2);
let temp = word1;
word1 = word2;
word2 = temp;
print(word1, word2);
```

这个程序的输出是:

```
apple aardvark
aardvark apple
```

现在让我们检查一个不同的模板，它将让我们有机会使用 JavaScript 的算术运算符——*提取数字*模板。

# 提取数字程序模板

在我们介绍提取数字模板背后的技术和模板本身之前，让我们先谈谈为什么要从一个数字中提取数字。一个应用是当一个号码被用作识别。一个识别方案可以由三个数字组成，后面跟着第四个数字，称为校验位。该数字用于确保识别号有效。一种方法是将第四个数字作为前三个数字的总和。为了能够确定这一点，我们必须有办法从一个数字中提取所有的数字。现在让我们看看提取数字的技术和模板。

*提取数字*模板背后的概念是，当你取一个数的模数 10 时，余数就是那个数字。以下是一些使用 JavaScript shell 的示例:

```
js> 1 % 10
1
js> 4 % 10
4
js> 6 % 10
6
js> 9 % 10
9
js> 10 % 10
0
```

然后，如果你把这个数除以 10，并且只使用整数结果，你将得到这个数减去最后一个数字。同样，下面是 shell 中的一些示例:

```
js> parseInt(23 / 10)
2
js> parseInt(125 / 10)
12
js> parseInt(4375 / 10)
437
```

记住这些技术，我们现在可以定义一个模板来提取一个数字中的所有数字。下面是伪代码:

*当数除以 10 大于 0 时循环:
将数的模 10 存储在变量中
整数除以 10*

下面是一个程序，它获取一个数字并提取它的数字:

```
let number = 432;
let digits = [];
while (number > 0) {
  digits.push(number % 10);
  number = parseInt(number / 10);
}
print(digits.reverse());
```

这个程序的输出是:

```
4,3,2
```

# 找出三个或更多数字的最小值和最大值

另一个常见的编程任务是找到一组数字的最小值和最大值。找出两个数字的最小值和最大值很简单，但是当比较三个或更多的值时，逻辑就变得复杂了。在本节中，我们将向您展示两种不同的模板，用于查找两个以上数字的最小值和最大值。

让我们从寻找三个数的最小值和最大值开始。下面是查找最大值的模板:

*如果第一值大于第二值且第一值大于第三值
，则第一值为最大值
，否则如果第二值大于第一值且第二值大于第三值
，则第二值为最大值
，否则如果第三值大于第一值且第三值大于第二值
，则第三值为最大值*

下面是实现该模板的程序:

```
let max = 0;
putstr("Enter first value: ");
let fval = parseInt(readline());
putstr("Enter second value: ");
let sval = parseInt(readline());
putstr("Enter third value: ");
let tval = parseInt(readline());
if (fval > sval && fval > tval) {
  max = fval;
}
else if (sval > fval && sval > tval) {
  max = sval;
}
else if (tval > fval && tval > sval) {
  max = tval;
}
print("The maximum value is", max);
```

下面是该程序三次运行的输出:

```
C:\js>js test.js
Enter first value: 23
Enter second value: 11
Enter third value: 12
The maximum value is 23C:\js>js test.js
Enter first value: 12
Enter second value: 123
Enter third value: 99
The maximum value is 123C:\js>js test.js
Enter first value: 1
Enter second value: 2
Enter third value: 3
The maximum value is 3
```

您可以对最小值做同样的事情，只需将条件的逻辑从大于改为小于。

实现该模板的另一种方法是创建一个函数，其中的值表示为该函数的 rest 参数。然后，您可以编写一个实现该模板版本的循环，该实现将适用于任意数量的值:

*将最大值设置为数组的第一个元素。
从第二个元素开始循环数组:
如果当前元素大于 max-value:
max-value 获取当前元素的值*

下面的程序演示了这种实现是如何工作的:

```
function greatest(...args) {
  let max = args[0];
  for (let i = 1; i < args.length; i++) {
    if (args[i] > max) {
      max = args[i];
    }
  }
  return max;
}putstr("Enter first value: ");
let fval = parseInt(readline());
putstr("Enter second value: ");
let sval = parseInt(readline());
putstr("Enter third value: ");
let tval = parseInt(readline());
let max = greatest(fval, sval, tval);
print("The maximum value is", max);
```

下面是该程序运行一次的输出:

```
C:\js>js test.js
Enter first value: 12
Enter second value: 11
Enter third value: 10
The maximum value is 12
```

# 最后的想法

程序模板不必是适用于许多不同编程场景的通用模板。模板可以有非常具体的功能，之所以被认为是模板，是因为它为许多不同编程环境中的常见问题提供了解决方案。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***