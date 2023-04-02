# 2 个 JavaScript 项目“你”可以轻松完成

> 原文：<https://javascript.plainenglish.io/2-javascript-projects-you-can-easily-do-fb4d5d144a06?source=collection_archive---------11----------------------->

![](img/0bab5fa2d5c5750a75295e7932093c8d.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript-code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

这里有两个 JavaScript 项目，只要对 JavaScript 有一个大致的了解，你就可以很容易地完成。

# 1.使用颜色选择器更改背景颜色

第一个很容易做。所以，这个项目是你可以接受一种颜色作为输入，并改变背景颜色，在这个例子中，是 body 标签。通过将`input`标签的类型属性设置为“color ”,颜色选择器获取输入。是的，`input`标签有颜色类型。看下面这支笔。

正如你所看到的，首先，我们定义了一个变量`color_picker`来选择`input`标签，这是一个颜色选择器(类型属性设置为“颜色”的`input`标签自动生成一个颜色选择器)。我们将它定义为获取作为未来输入的颜色值。

现在，我们用函数`changecolor()`为输入设置一个输入事件监听器，这意味着只要给出一个输入(这里输入指的是`input`标签)，就会触发`changecolor()`函数。

现在，让我们定义一下`changecolor()`函数。首先，我们将通过`color_picker.value`语句获取输入中选择的颜色，并将其存储在`selected_color`变量中。然后我们通过`document.getElementsByTagName("body")[0]`语句选择 body 标签。基本上，`document.getElementsByTagName`获取所有具有已定义标签名称的标签，并将其存储到一个数组中，通过在`document.getElementsByTagName("body")`之后使用`[0]`，我们选择标签名称为“body”的第一个标签。由于在整个 HTML 文档中只有一个“body”标签，我们可以准确地选择 body 标签，这种方法对于选择某个标签可能是有用的，但是`document.getElementById`方法没有那么混乱。现在，为了方便起见，您可以将`document.getElementsByTagName("body")`存储在一个变量中，但这不是强制性的。

现在通过`document.getElementsByTagName("body")[0].style.backgroundColor = selected_color;`将存储在`selected_color`变量中的所选颜色设置为背景颜色属性。这是你的第一个项目。

# 2.计时器或秒表

现在对于第二个项目，它是一个计时器或秒表。许多程序员发现制作一个定时器令人生畏和困惑，但相信我，这是一个容易的项目。这个项目的解释很长，因为如果你没有足够的信息，某些事情会让你担心。先看下面这支笔，试着理解代码。

首先，你可以随意设计计时器的布局，但是每个数字都要分开。现在给每个数字不同的 id，这样我们就可以分别选择它们。

现在用`document.getElementById`方法存储变量中的所有数字，并用`parseFloat(variable_name_of_the_digit.innerHtml)`方法存储变量中所有数字的个数。`variable_name_of_the_digit`是你用来存储数字的变量的名字，你应该使用`parseFloat`，因为`.innerHtml`返回一个字符串，你不能增加一个字符串，所以它会把字符串转换成一个数字，这样我们就可以增加它。

现在创建一个函数来增加秒的第一个数字(右边的一个)。首先，编写`variable_name_of_the_innerHtml_of_the_first_digit_of_seconds++;`语句来增加秒的第一个数字。`variable_name_of_the_innerHtml_of_the_first_digit_of_seconds`是您用来存储秒的第一个数字的`innerHtml`的变量名。变量名后的`++`将增加(加 1)数字。现在将秒的第一个数字的`innerHtml`设置为`variable_name_of_the_innerHtml_of_the_first_digit_of_seconds`。这意味着秒的第一个数字每秒钟增加 1。

现在将秒的第一个数字改为 0，第二个数字每 10 秒递增一次。我们将首先使用一个`if`语句来检查秒的第一个数字是否是 9。然后在`if`内部，我们将把`variable_name_of_the_innerHtml_of_the_first_digit_of_seconds`设置为-1。不要将其设置为 0，因为下一秒它将增加到 1，数字将显示 1 而不是 0，但使用-1 时，它将显示 0 而不是 1。

接下来，我们将秒的第二位(左边一位)的值增加`variable_name_of_the_innerHtml_of_the_second_digit_of_seconds++`，然后将第二位的`innerHtml`设置为该值。

现在，为了每 60 秒改变秒 0 的两位数，我们将首先使用一个`if`语句，对于`if`语句的条件，我们将传递秒的第一位(右一位)是 9，秒的第二位(左一位)是 5 的条件。然后在`if`语句中，只需将`variable_name_of_the_innerHtml_of_the_second_digit_of_seconds`设置为-1(同样不要将其设置为 0)。没有必要将它设置为秒的第二位的`innerHtml`，因为前面的`if`语句已经这样做了。现在秒机制的功能完成了。

现在，对于分钟的机制，只需复制我们为秒钟创建的函数，将秒钟的变量名改为分钟，并将函数名改为分钟。现在机制的功能就这样完成了。

对于小时，再次复制相同的函数，将用于分钟的变量名称改为小时，并删除将两位数字重置为 0 的`if`语句，因为计时器中没有日期。

***注意:*** *不要改变所有函数里面语句的顺序。*

现在要启动计时器，只需创建一个按钮并给它一个 id。然后使用`document.getElementById`方法创建一个变量来选择按钮，然后声明三个变量来存储三个函数的`setInterval`，但是在任何函数之外声明这些变量，并且只声明。我们稍后将把这些变量中的`setInterval`存储在定时器启动、停止和重置机制的函数中。

声明这些变量后，只需创建一个函数。在这个函数中写一个`if`语句，条件应该是当定时器为 0 时，按钮的`innerHtml`等于按钮内的文本，在我的例子中是“启动定时器”。然后在这个`if`语句中，初始化三个变量来存储三个函数的`setInterval`，分别使用`variable_name_for_setInterval_of_second_function = setInterval(function_name_for_second, 1000);`、`variable_name_for_setInterval_of_minute_function = setInterval(function_name_for_minute, 60000);`和`variable_name_for_setInterval_of_hour_function = setInterval(function_name_for_hour, 3600000);`来存储秒函数、分函数和小时函数，其中`variable_name_for_setInterval_of_second_function`、`variable_name_for_setInterval_of_minute_function`和`variable_name_for_setInterval_of_hour_function`分别是您只为秒函数、分函数和小时函数的`setInterval`声明的变量名称，`function_name_for_second`、`function_name_for_minute`和`function_name_for_hour`分别是不带括号的秒函数、分函数和小时函数的名称。然后同样在当前的`if`语句中，当按钮用于停止定时器时，将开始、停止和复位按钮的`innerHtml`设置为您想要的文本，然后写入`return`。

然后再写一个`if`语句，其中的条件是按钮的`innerHtml`等于按钮用于停止定时器时你想要的文本在我这里是“停止定时器”。在这个`if`语句中，只需用`clearInterval(variable_name_for_setInterval_of_second_function)`、`clearInterval(variable_name_for_setInterval_of_minute_function)`和`clearInterval(variable_name_for_setInterval_of_hour_function)`分别清除秒、分、小时函数的`setInterval`来清除前面`if`语句中三个函数的`setInterval`。之后，只需将按钮的`setInterval`设置为您选择的文本，当按钮准备好重置计时器时，在我的情况下，它是“重置计时器”，并在此语句后写入`return`。

现在，为了重置计时器，定义另一个`if`语句，这一次的条件是，当按钮准备好重置计时器时，按钮的`innerHtml`等于您选择的文本，在该`if`语句中，将所有数字设置为 0。

现在，通过使用 HTML 中的`onclick`属性或 JavaScript 中的按钮上的`addEventListener`,向按钮添加用于启动、停止和重置计时器的函数。

***注意:*** *写作*`*return*`*`*if*`*语句的结尾很重要；否则，点击按钮时的启动、停止和复位机制将不起作用。原因在我的另一篇文章里有解释。**

*这里有两个使用 JavaScript 的简单项目。我希望这些能对你的编程之旅有所帮助，并对你想写的文章的主题提出建议。如果代码的冗长解释给你带来不便，我深表歉意！*

*再见。*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。******