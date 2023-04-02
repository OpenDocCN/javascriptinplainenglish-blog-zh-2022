# 如何执行存储在字符串中的 JavaScript 代码？

> 原文：<https://javascript.plainenglish.io/how-to-execute-javascript-code-stored-in-a-string-6aff91c7590e?source=collection_archive---------3----------------------->

![](img/5ee3be8d9ac8542bae3c598006506741.png)

Photo by [Bruno Nascimento](https://unsplash.com/@bruno_nascimento?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们有一个 JavaScript 字符串，其中包含我们想要运行的代码。

在本文中，我们将研究如何执行存储在字符串中的 JavaScript 代码。

# 用函数构造器创建一个新函数

我们可以用`Function`构造函数从 JavaScript 代码串中创建一个新函数。

例如，我们可以写:

```
const code = "alert('Hello World'); let x = 100";
const F = new Function(code);
F();
```

创建代码串并将其存储到`code`变量中。

然后我们将`code`传递给`Function`构造函数，从中创建一个函数。

然后我们调用`F`来运行这个函数。

# 使用 setTimeout 函数

我们还可以将 JavaScript 代码串传入`setTimeout`函数来运行代码串。

为此，我们写道:

```
const code = "alert('Hello World'); let x = 100";
setTimeout(code, 1);
```

我们将`code`作为`setTimeout`函数的第一个参数来运行它。

第二个参数是运行该函数之前的延迟(毫秒)。

# 不要使用 eval 函数

我们不应该使用`eval`函数从字符串中运行代码。

这是因为任何人都可以轻松地向其中注入代码，这是一个很大的安全风险。

此外，它创建了自己的作用域，这意味着它可能会做我们意想不到的事情。

所以我们不应该写这样的代码:

```
const code = "alert('Hello World'); let x = 100";
eval(code)
```

在我们的 JavaScript 代码中。

# 结论

我们可以用 JavaScript 运行存储在字符串中的 JavaScript 代码，方法是用`Function`构造函数创建一个函数，或者将它传递给`setTimeout`函数。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*