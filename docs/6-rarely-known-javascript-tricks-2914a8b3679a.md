# 6 个鲜为人知的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/6-rarely-known-javascript-tricks-2914a8b3679a?source=collection_archive---------6----------------------->

## 学习这些有用的技巧，让你的代码更简洁。

![](img/ac92b7fb27434be5a4d551cb4912a7bf.png)

Credit due to Bia Sousa

JavaScript 中有一些很少使用但很有用的技巧，现在就学习吧！

如题，不再多言，直入主题吧！

## 1.数组操作:

我们每天都要进行大量的阵列操作，下面是一些可以尝试的基本技巧:

a.使用`reduce()`计算总和、乘积:

b.使用`reduce()`找到最大值/最小值:

c.使用`some()`和`every()`检查条件:

例如，让我们检查是否所有的元素都在我们的数组中:

我们可以使用`some()`来检查数组中的某个元素是否满足条件:

## 2.信息丰富的控制台日志:

当你试图在控制台记录一些东西时，下次你可以用`{}`包装你的变量，你会看到控制台会以字典的形式打印出变量名及其值。非常好用！

## 3.信息数字格式:

对用 JavaScript 写大数字感到困惑？用`_`把他们劈开，看看会发生什么！

但是要小心！一些版本的 JavaScript 编译器不支持它。所以最好在提交代码之前仔细检查一下！

## 4.简单交换:

交换两个没有临时号码的号码:

## 5.用 length 属性缩短数组:

想要保留数组中的前 n 个元素吗？没问题！

## 6.没有 if 的条件:

有一个漂亮的方法可以捕捉到`if (condition) {doSomething();}` = > `condition && doSomething();`请看下面的例子:

以上是 6 个曝光率较低但绝对值得一看的技巧。请随意查看并探索更多 JavaScript 技巧！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***