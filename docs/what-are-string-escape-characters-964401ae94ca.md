# JavaScript 字符串转义字符

> 原文：<https://javascript.plainenglish.io/what-are-string-escape-characters-964401ae94ca?source=collection_archive---------7----------------------->

## 如何使用字符串转义字符—举例说明。

![](img/d1e2a1654184203369b20fd6cbf459dd.png)

## 介绍

如果你想看这篇文章旁边的视频，可以在下面找到。

在 JavaScript 中，当我们处理字符串时，有时我们希望以某种方式分解字符串。我们有一些转义字符可以用来帮助我们应对这个挑战。

*   \' **单引号**
*   \" **双引号**
*   \n **换行符**
*   \\ **反斜杠**

## 引用

处理字符串时，如果要在字符串中使用引号，则字符串中的引号不能与字符串中的引号相同。让我们看一些例子。

```
const quote = "A famous quote is "I think, therefore I am" "
//Returns ---> Uncaught SyntaxError: Unexpected identifierconst secondQuote = 'A famous quote is 'I think, therefore I am' ';
//Returns ---> Uncaught SyntaxError: Unexpected identifier
```

在上面的例子中，我们首先声明一个标识符为 *quote* 的变量，然后给这个变量分配一个用双引号括起来的字符串，这个字符串包含一个也用双引号括起来的引号。接下来，我们创建第二个名为 *secondQuote* 的变量，再次重复相同的步骤，但这次它使用单引号。这两种方法都会返回语法错误。解决这个问题的一种方法是对报价使用不同的引号，如下例所示。

```
const quote = "A famous quote is 'I think, therefore I am' "
const secondQuote = 'A famous quote is "I think, therefore I am" ';
```

在上面的例子中，存储在变量 *quote* 中的字符串对引号使用单引号，对字符串使用双引号。 *secondQuote* 变量的字符串使用单引号，引号使用双引号。这两种方法都有效。或者，我们可以使用转义字符，如下例所示。

```
const quote = "A famous quote is \"I think, therefore I am\" "
const secondQuote = 'A famous quote is \'I think, therefore I am\' ';
```

在上面的例子中，我们在存储在 *quote* 变量中的字符串的开头和结尾使用了反斜杠和双引号。我们重复相同的步骤，但是我们对存储在 *secondQuote* 变量中的字符串使用反斜杠和引号。

另一个有用的时候是如果你想在字符串中使用撇号。

```
const phrase = 'You\'ve had eight cookies';
//Returns ---> "You've had eight cookies"
```

## **换行符**

当您想要将字符串分成多行时，一个可用的选项是使用换行符。我们把它放在我们希望新行出现的地方。让我们看一个例子。

```
"Monday, Tuesday, Wednesday";
//Returns ---> 'Monday, Tuesday, Wednesday'"Monday,\nTuesday,\nWednesday";
//Returns ---> 
"Monday,
Tuesday,
Wednesday"
```

## 反斜线符号

如果你想在字符串中使用反斜杠，你需要使用两个反斜杠字符。假设我们在使用转义字符时使用了反斜杠，我们不能在一个字符串中只使用一个反斜杠。让我们看一些例子。

```
"Hello \";
//Returns ---> Uncaught SyntaxError: Invalid or unexpected token"Hello \\";
//Returns ---> 'Hello \'
```

我希望你喜欢这篇文章。请随时发表任何评论、问题或反馈，并关注我以获取更多内容！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**