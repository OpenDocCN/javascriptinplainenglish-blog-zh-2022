# JavaScript 中的' typeof '运算符是什么？

> 原文：<https://javascript.plainenglish.io/what-is-the-typeof-operator-888a490e6902?source=collection_archive---------15----------------------->

## 如何在 JavaScript 中使用“typeof”运算符

![](img/2095f7988a622267768dd149c3a8d4ab.png)

您可以使用`typeof`操作符来找出特定值的类型。这个操作符全部是小写的，使用它的时候，你可以使用`typeof`,后跟一个空格，然后是你想要找到的类型的值。不要使用括号，因为它不是一种方法。当您使用运算符时，返回值将是值的类型，但它将作为字符串返回。让我们来看一些例子:

```
typeof 6;
//Returns ---> 'number'typeof "Hello";
//Returns ---> 'string'typeof true;
//Returns ---> 'boolean'typeof undefined;
//Returns 'undefined'
```

您可以使用`typeof`来检查存储在变量中的值的类型，如下例所示。

```
const name = "Ben";
typeof name;
//Returns ---> 'string'
```

在上面的例子中，我们声明了一个名为 *name* 的变量，并用字符串 *Ben* 对其进行初始化。当我们使用`typeof`操作符和变量*名称*时，我们得到返回的字符串，因为这是存储在变量中的值的类型。

当您对某些类型使用`typeof`操作符时，有一些行为值得注意。当您检查 null 的类型时，您将得到一个返回 object 的字符串。这被认为是 JavaScript 的一个怪癖。让我们来看一个例子:

```
typeof null;
//Returns ---> 'object'
```

让我们再看几个例子:

```
function myFunction() {
  return 1;
}typeof myFunction;
//Returns ---> 'function'const ourArray = [];
typeof ourArray;
//Returns ---> 'object'const ourObject = {};
typeof ourObject;
//Returns ---> 'object'
```

我希望你喜欢这篇文章，请随时发表任何意见，问题或反馈，并关注我的更多内容！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***