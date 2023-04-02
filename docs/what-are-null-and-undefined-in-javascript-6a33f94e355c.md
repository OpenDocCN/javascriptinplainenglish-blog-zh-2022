# JavaScript 中什么是 Null & Undefined？

> 原文：<https://javascript.plainenglish.io/what-are-null-and-undefined-in-javascript-6a33f94e355c?source=collection_archive---------5----------------------->

## 初学者对原始值“null”和“undefined”的介绍。

![](img/5c757b5483983b59f7ccdcf91d04a202.png)

在 JavaScript 中，null 和 undefined 是原始值。如果你想了解更多关于原始值的信息，你可以看这篇文章。由于 null 和 undefined 是原始值，我们可以在控制台中直接使用它们。让我们试一试。

```
null//Returns ---> nullundefined//Returns ---> undefined
```

我们也可以用`const`、`let`或`var`创建变量，并将它们设置为空或未定义。让我们快速浏览一下。

```
let first = null;
var second = null;
const third = null;console.log(first);
//Returns ---> nullconsole.log(second);
//Returns ---> nullconsole.log(third);
//Returns ---> null
```

在上面的例子中，我们用`let`、`var`和`const`声明了三个变量*第一个*、*第二个*、*第三个*。我们给每个变量赋值为 null。当我们`console.log`这个变量时，我们每次都得到一个 null 返回。让我们做同样的事情，但是这次使用 undefined。

```
let first = undefined;
var second = undefined;
const third = undefined;console.log(first);
//Returns ---> undefinedconsole.log(second);
//Returns ---> undefinedconsole.log(third);
//Returns ---> undefined
```

## 空

首先，我们来看看 null。Null 不代表任何东西，所以只是一个非值。例如，如果你打开冰箱找牛奶，但是里面没有，你可以说这是空的。在 JavaScript 中，我们通常有意设置 null。所以你可以创建一个变量来存储这个值，在这种情况下，我们可以称它为 *fridgeHasMilk* ，你可以给这个变量赋值 null。

```
const fridgeHasMilk = null;
console.log(fridgeHasMilk);//Returns null
```

在上面的例子中，我们首先使用`const`声明一个名为 *fridgeHasMilk* 的变量。然后我们给这个变量赋值 null。当我们`console.log`了 *fridgeHasMilk* 变量时，我们得到了 null 返回。

## 不明确的

另一方面，Undefined 也表示没有值，但是很少给变量赋值。它可以以错误的形式返回给我们，或者如果我们声明了一个变量，我们给了一个变量一个名字，但是我们没有通过给变量赋值来初始化它。让我们再次尝试上面的例子，但是这次我们不会用一个值来初始化变量。

```
let fridgeHasMilk;
console.log(fridgeHasMilk);//Returns ---> undefined
```

在上面的例子中，我们使用`let`创建了一个名为 *fridgeHasMilk* 的变量。我们不用任何值来初始化变量。我们然后`console.log`变量的值。我们得到 undefined 返回，因为变量没有定义任何值。

注意当你使用 const 时，你不能声明一个没有用值初始化的变量，你只能用`let`或`var`这样做。如果你用`const`做这个尝试，你会得到一个错误。

```
var fridgeHasMilk;
console.log(fridgeHasMilk);//Returns ---> undefinedconst fridgeHasMilk;
//Returns ---> Uncaught SyntaxError: Missing initializer in const declaration
```

我们对变量 *fridgeHasMilk* 重复上面例子中的相同步骤。我们第一次使用`var`。这和我们使用`let`时的工作方式是一样的，当我们`console.log`变量时，我们得到未定义的返回。稍后我们再次尝试相同的步骤，但是我们使用 const。在我们试图对变量进行`console.log`之前，我们得到了一个未被捕获的语法错误，它指出在`const`声明中缺少初始化器。如果你想更深入地理解这背后的原因，你可以阅读这篇关于[提升](https://blog.devgenius.io/introducing-hoisting-in-javascript-922faf4b37c9)的文章，但是你必须在创建变量时给用`const`创建的变量赋值。

## 例子

您可能会看到 undefined 的一种情况是，如果您正在处理一个字符串，并且您正在寻找一个不存在的元素。如果以弦冰为例。由于字符串是零索引的，如果我们使用括号符号在字符串中查找第 4 个字母，我们将得到未定义的返回，因为字符串 ice 只有 3 个字母，索引从零开始计数，没有第 4 个字母。

```
let ourString = "ice";
ourString[3];//Returns ---> undefined
```

在上面的例子中，我们使用`let`创建了一个名为 *ourString* 的变量。我们用字符串 ice 初始化这个变量。接下来，我们尝试访问字符串的第四个字母。我们使用括号符号来实现，因为字符串是零索引的，所以我们将 3 传递到括号中。字符串的第四个字母不存在，所以我们得到 undefined 返回。

我在这里制作了这篇文章的视频:

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*