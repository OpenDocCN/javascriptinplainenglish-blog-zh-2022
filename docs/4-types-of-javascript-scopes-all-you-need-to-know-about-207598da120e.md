# 4 种 JavaScript 作用域——您需要知道的全部

> 原文：<https://javascript.plainenglish.io/4-types-of-javascript-scopes-all-you-need-to-know-about-207598da120e?source=collection_archive---------20----------------------->

我看到很多前端开发人员不确定什么是作用域，即使他们每天在工作中使用它。我决定简化术语“范围”,让您更好地理解这个重要术语。

![](img/397a81952dce2146e7226446bfe4e7cb.png)

# 领域

我们将经历 4 种类型的范围。

# 局部范围

特定函数中的任何变量或函数都称为特定函数的局部作用域。

```
function localScope(){
  var name="David"; //Local scope of the function.
}
```

# 功能范围

任何函数都有自己的作用域，这意味着什么？这意味着特定函数内部的所有变量或函数对于外部函数都是不可访问/不可见的，它们对于函数来说是局部的。

```
//The variable 'name' can't be used here.function innerScope(){
  //Start of function scope
  var name = "David";
  //Local scope.
  console.log(name); //Will print to the console "David".
  //End of function scope.
}//The variable 'name' can't be used here.
```

在上面的例子中，你可以看到变量`name`在一个函数范围内。变量`name`只能从函数本身访问，对外部的其他函数不可见，例如:

```
function innerScope(){ 
  var name = "David";
}
console.log(name); //Error, Uncaught ReferenceError: name is not defined
```

通过执行`console.log(name)`，我们将收到一个错误`Uncaught ReferenceError: name is not defined`。这是因为变量`name`不在函数范围内。

# 全球范围

这种类型的作用域是在任何函数外部声明变量。这样，任何函数都可以使用该变量。这就是为什么这样的变量会出现在**全局作用域**中。

当变量是全局变量时，您可以在代码中的任何地方使用它。

```
var name="David"; //Global scope.
//The 'name' variable can be used here.function printNameFromGlobalScope(){
  console.log(name); //Will print to the console "David".
}//The 'name' variable can be used here.
```

正如你在上面的例子中看到的，变量`name`是在函数`printNameFromGlobalScope()`之外声明的，所以即使它没有在函数内部声明，我们也可以访问它。有可能，因为它是在全局范围内声明的。

# 高级提示

如果一个局部变量和一个全局变量有相同的名字，那么它们不会互相覆盖。

```
var name="David"; //Global scope.function printName(){
  var name="Arik"; //Local scope.
  console.log(name); //Will print to the console "Arik".
}console.log(name); //Will print to the console "David".
```

# 自动全局

我们将经历的最后一种类型的作用域是自动全局的。

当对一个函数的调用包含对一个从未在特定函数中声明的变量的赋值时，自动发生全局作用域。

```
function print automaticallyGlobalName(){
  name="David"; //No let, var or const before assignment a value.
  console.log(name); //Will print to the console "David".
}automaticallyGlobalName();
console.log(name); //Will print to the console "David".
```

请注意上面示例代码中的步骤。首先，声明函数。第二，有一个变量的赋值从未被声明。第三，我们调用这个特殊的函数。最后，我们打印出`name`变量。

第三步很重要，因为如果我们跳过这一步，我们就会收到`undefined`。这是因为如果我们不通过它，我们就不能将`name`添加到全局范围。所以当我们调用`automaticallyGlobalName`函数时，编译器会注意到`name`变量从未被声明，并将其添加到全局范围。

**感谢**到目前为止的阅读，如果你喜欢这样的内容，并且你想支持我作为一个程序员和作家写更多像这样的文章， [***请用我的链接注册成为 Medium 的会员(5 美元/月订阅)，你将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

这就是现在，希望你喜欢这篇文章。

关注我，获取更多有趣且有帮助的文章。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***