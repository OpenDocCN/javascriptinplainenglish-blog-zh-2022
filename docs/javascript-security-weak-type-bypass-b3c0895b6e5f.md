# JavaScript 安全性—弱类型旁路

> 原文：<https://javascript.plainenglish.io/javascript-security-weak-type-bypass-b3c0895b6e5f?source=collection_archive---------15----------------------->

## 黑客如何利用弱类型特性绕过 JavaScript 安全检查。

![](img/b270e7e5b580575f03085ed2bd56a3e4.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您可能知道，JavaScript 是一种弱类型语言。黑客可以利用该语言的这些特性绕过 Node.js 应用程序中的一些检查。那么，弱型是什么意思呢？让我们考虑下面的例子:

```
var a =1;
var b ="1";
var c= a + b;
console.log(c==="11");  //return True
```

因此，在上面的例子中，如果一个整数被一个字符串添加，而不是抛出一个错误，整数将被转换为字符串并附加在它上面。因此，在 JavaScript 中，它的数据类型可能会在计算过程中发生变化。这就是我们称 JavaScript 为弱类型语言的原因。

但是黑客如何利用这些特性呢？现在，让我们看看下面这个简单的例子:

```
let username = "Peter";if (username === "admin")
{
    console.log("access denied!");
}
else
{
     console.log("hello "+username);   //output: hello Peter
}
```

所以，这个应用程序很简单。应用程序检查用户是否是管理员。如果是，打印“拒绝访问！”。如果没有，打印“你好{用户名}”。那么，有没有什么方法可以绕过这个检查，强制应用程序打印“hello admin”呢？。答案是肯定的！

如上所述，===意味着类型和内容必须相同。例如:

```
"admin" === "admin" //return True
"admin" === ["admin"] //return False
```

在上面的情况中，第一行代码返回 True，因为类型和内容是相同的。第二行代码返回 false，因为它将一个字符串与一个列表进行比较。

容易吗？我们继续。

现在，我们尝试如下所示:

```
let greeting1 = "Hi "+"admin";
let greeting2 = "Hi "+["admin"];greeting1===greeting2 //return True
```

现在，如果我们将字符串和列表附加到同一个字符串，并比较它们的输出。你会发现它返回真。这是因为当列表被附加一个字符串时，它也变成了一个字符串。所以，要绕过这个，很简单。只需将用户名设置为["admin"]，如下所示:

```
let username = ["admin"];if (username === "admin")
{
    console.log("access denied!");
}
else
{
     console.log("hello "+username);   //output: hello admin
}
```

看到了吗？你可以就这样绕过。

# 结论

这一招是开发者很容易忽略的。因此，如果您正在进行黑盒测试，尝试将您的输入从字符串更改为列表以查看是否可以绕过某种检查总是值得的。在源代码审查中，检查是否有一些代码具有上述行为总是好的，这些行为允许您构造一个有效载荷来绕过一些检查。希望你喜欢这篇文章和快乐的黑客！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。**