# JavaScript 中的 parseInt()是什么

> 原文：<https://javascript.plainenglish.io/what-is-parseint-in-javascript-5d1aba3fdf9c?source=collection_archive---------15----------------------->

## 了解如何在 JavaScript 中使用 parseInt()函数

![](img/895af8826c17b5ec55a171fb883343b3.png)

## parseInt()简介

parseInt()函数是 JavaScript 中的一个全局函数。这意味着我们可以直接调用函数。当我们想把一个字符串转换成一个整数(数字)时，我们使用函数。函数的参数接受一个需要转换(或解析)为整数的字符串。函数的返回值是整数。让我们看一个基本的例子:

```
let stringTwenty = '20';
parseInt(stringTwenty);//Returns ---> 20
```

在上面的例子中，我们声明了一个变量，我们给它一个标识符*string wenty*。我们用一个包含 *20* 的字符串初始化这个变量。当我们使用 *parseInt* 函数时，我们将变量作为参数传递给参数。返回值是整数 20。

## 非数字首字符

使用 parseInt 时，需要注意一些事项。如果传递给函数的第一个字符是一个非数字值(例如一个字母字符),因此不能更改，将返回 NaN(非数字)。让我们来看一个例子:

```
let drink = "tea";
parseInt(drink);//Returns ---> NaN
```

在上面的例子中，我们声明了一个名为 *drink* 的变量，并用字符串 *tea* 对其进行初始化。当我们使用 parseInt 函数时，我们将 *drink* 变量作为参数传入。没有要解析的整数，所以我们得到了返回的 *NaN* (不是一个数字)。如果您的字符串包含一个数字，但以一个字母或单词开头，我们会得到相同的行为。这显示在以下示例中:

```
let classroom = "a2";
parseInt(classroom);//Returns ---> NaN
```

## 以数字开头的字符串

如果传递给函数的值以一个数字开始，以一个字符串结束，你将得到这个字符串的数值。让我们来看一个例子:

```
let days = "20 days";
parseInt(days);//Returns ---> 20
```

在上面的例子中，我们声明了一个名为 *days* 的变量，它是用一个以 *20* 开始但以一个单词结束的字符串初始化的。当我们将 *days* 变量传递给 *parseInt()* 函数时，我们得到了返回的 *days* 字符串的整数部分。

## 漂浮物

如果你传入一个浮点数(一个带小数的数字),只有整数部分的值会被返回，并且它会停止在小数部分。让我们来看一个例子:

```
let twentyDecimals = "20.22";
parseInt(twentyDecimals);//Returns ---> 20
```

在上面的例子中，我们声明了一个名为 *twentyDecimals* 的变量。我们用一个包含浮点数(20.22)的字符串初始化变量。当我们将 *twentyDecimals* 作为参数传入调用 *parseInt()* 时，我们只得到返回的小数之前的值。

我希望你喜欢阅读这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*