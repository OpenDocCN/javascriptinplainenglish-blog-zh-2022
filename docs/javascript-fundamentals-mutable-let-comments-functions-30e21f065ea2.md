# JavaScript 基础:可变字母、注释、函数

> 原文：<https://javascript.plainenglish.io/javascript-fundamentals-mutable-let-comments-functions-30e21f065ea2?source=collection_archive---------11----------------------->

## # 100 日代码的第 2 天

![](img/d189fb3dfa2dcf1eddd947a970332aa5.png)

今天是我的 JavaScript 之旅的第二天。

我将通过我的博客和社交活动，用一种解释的方式写下我的所学。如果你想加入我的学习之旅，一定要关注我的博客和社交网站，并分享你的博客和社交网站。**一起学习吧！🫱🏼‍🫲🏼**

本文是 [JavaScript 基础](https://astrodevil.hashnode.dev/series/js-fundamentals)系列**的一部分。**

# 可变字母

我们在上一节讨论了变量，现在进一步讨论变量，我们如何改变变量内部的存储值？

我们使用了`const`关键字来声明一个常量变量，但是如果我们试图改变它的值，就会出错。

```
const a = 4;
a = 8;
```

如果我们试着跑到这条线以上，它会给出`TypeError: Assignment to constant variable`。常数是不可变的，这意味着它们的值不能改变。

这里出现了关键字`let`，它允许值是可变的(意味着它可以改变)。

```
let a = 4;
a = 8;
```

上面的代码将会正确运行。

# 评论

评论是节目的重要组成部分。写好的注释对于成为一名优秀的程序员和写出干净的代码也是必要的。

想出好的变量名也很重要。

```
const value = 99;
const price = 99;
```

两者持有相同的值`99`，但是`price`更具描述性。

注释只是为了人类更好地理解代码。我们可以写单行或者多行注释。

```
// this is price in U.S. Dollars
const price = 99;
```

```
/* The price of all items
   Denominated in U.S. Dollars  */
const price = 99;
```

# 功能

函数是可重用的代码，它返回一个输出。函数必须在调用之前定义。函数调用意味着执行函数。单词 *invoke* 也被使用，意思与 call 相同。

当一个函数被调用时，意味着你正在传递特定的输入值。

```
const output = addOne(5);
```

在上面的代码中，`addOne`是函数，圆括号`( )`用于调用函数。我们将输入值 5 传入函数 addOne。

函数中不一定要有输入值。参见下面的例子。

```
const message = getMessage();
```

为了调用一个函数，我们必须首先定义它！

```
function addOne(input) {
    return input + 2;
}
```

在上面的代码中，我们创建了一个名为`addOne`的函数，它接受一个名为 input 的输入。我们返回输入加 2。

```
function getMessage() {
    return "Hello World!";
}
```

在上面的代码中，函数`getMessage`不接受输入。我们只是返回一个字符串，说“Hello World！”。`return`语句将返回函数的期望输出。

```
const a = addOne(2);
```

变量`a`现在被赋给用输入 2 调用的`addOne`函数的返回值，其值为 4。

# 结论

以关于 JavaScript 函数的额外信息结束…

如果我们定义/声明一个函数，它可以在程序的其他地方被调用。

**今天我学习了 JavaScript 中可变字母、注释和函数。**如果你❤️我的内容！在推特[上联系我](https://mobile.twitter.com/Astrodevil_)或者通过[给我买一辆 Coffee☕](https://www.buymeacoffee.com/Astrodevil) 来支持我

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费每周简讯**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，** [**不和谐**](https://discord.gg/GtDtUAvyhW) **。**

## 对扩展您的软件启动感兴趣吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。