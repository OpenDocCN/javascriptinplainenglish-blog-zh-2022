# 如何在下一个 JavaScript 项目中轻松实现文本到语音的功能

> 原文：<https://javascript.plainenglish.io/how-to-easily-implement-text-to-speech-functionality-in-your-next-javascript-project-16f0d14432f0?source=collection_archive---------3----------------------->

## 没有时髦的装置。初学者友好的。用少于 5 行的代码完成它。

![](img/59dc348f796071231761c12501a6c79d.png)

Photo By [Oleg Laptev](https://www.instagram.com/oh.snowshade/)

嘿朋友们，

自从我们实现了一些非常酷的东西以来，这是一个非常热的时刻。最后一次大概是 2 月 12 日，你[和我](https://medium.com/javascript-in-plain-english/build-a-web-scraper-with-me-beginner-friendly-19d2d98ac8d1)一起做了一个 web scraper。

今天，我将快速向您展示如何用不到 5 行代码轻松实现文本到语音的功能。我目前正在为我的高级项目 [MataChat](https://github.com/sebastians1994/MataChat) 做这件事，因为其中一个需求是添加可访问性特性。请随意查看。

MataChat 是由一群大学高年级学生和硕士生组成的团队开发的——我们当中没有人知道实现文本到语音的功能有多容易。给我几分钟时间让你看看实现起来有多容易。

我们开始吧。

# 网络语音 API

首先，我们不需要在电脑上安装任何新奇的东西。我们将简单地使用 Web 语音 API 而且要使用这个 API，没有繁重的幕后过程。不需要导入任何东西。你就用吧！

## 语音合成接口

我们将从使用名为**语音合成**的 Web 语音 API 接口开始。这就是我们将界面引入项目的方式:

```
let utterance = new SpeechSynthesisUtterance();
```

运筹学

```
let utterance = new window.SpeechSynthesisUtterance();
```

两者达到相同的结果。选一个。

## 基本的文本到语音转换

对于文本到语音转换，我们希望将文本转换为语音。很明显。

比如说，我想把文字“Hello World”转换成语音。

第一步是创建一个**发音**。基本上，让界面知道你想发声什么。在我们的例子中，我们想说“Hello World”。这里有一些我们可以创造话语的方法。选一个。

```
// Take 1
let utterance = new SpeechSynthesisUtterance("Hello World");//Take 2
let message= "Hello World";
let utterance = new SpeechSynthesisUtterance(message);//Take 3
let utterance = new SpeechSynthesisUtterance();
utterance.text = "Hello World";//Take 4
let utterance = new SpeechSynthesisUtterance();
utterance["text"]= "Hello World";
```

所有这些都会产生相同的最终结果。做任何对你有意义的事。选一个。

至此，我们有了一个话语。我们告诉界面我们想说什么。现在我们必须告诉界面开始发出我们的声音。基本上就是告诉界面开始说话。为此，我们将使用界面的 speak 功能。它将如下所示:

```
speechSynthesis.speak(utterance);
```

注意，speak 函数的参数是我们的话语。当执行这一行时，“Hello World”将被转换为语音。

以下是其他一些例子:

```
let utterance = new SpeechSynthesisUtterance("Hello There");
speechSynthesis.speak(utterance);let spokenWord= new SpeechSynthesisUtterance("Hello Adam");
speechSynthesis.speak(spokenWord);let message= new SpeechSynthesisUtterance("Hello Becky");
speechSynthesis.speak(message);
```

这是为了向您展示保存您的话语的变量可以被命名为您想要的任何名称(以防对我们的新开发人员来说不明显)。尽管它可以被命名为您想要的任何名称，但是您应该确保该名称有意义并且不言自明。如果其他人阅读你的代码，或者一年后你阅读你的代码，你的代码应该是有意义的。应该是**可读**和**可维护**。

现在你知道了！

# 密码笔

如果你想看到一个工作版本，看看这个代码笔。非常简单易懂。

当你点击按钮时，你应该会听到“你好，世界”

## 更新话语

```
let utterance = new SpeechSynthesisUtterance("Hello World");
speechSynthesis.speak(utterance);
```

这是我们到目前为止所拥有的。想象一下，在许多行代码之后，我们想要更新我们的话语，这样我们就可以说些别的了。你可以这样更新话语:

```
let utterance = new SpeechSynthesisUtterance("Hello World");
speechSynthesis.speak(utterance);utterance.text = "Goodbye World." //updates value
speechSynthesis.speak(utterance);
```

当然，你也可以创造一个新的话语；然而，这并不能有效利用内存空间。不要浪费内存空间。

## 自定义

你可以对演讲做一些修改。你可以改变音调、音量、语速，甚至声音。( [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesisUtterance))让我们来看看。

**【1】改变音高**

如果您想要改变说话时的音调，您可以降低或提高音调。默认情况下，音高值为 1。可接受的范围在 0 和 2 之间。

这里有一个例子:

```
let utterance = new SpeechSynthesisUtterance("Hello World");
utterance.pitch = 4; //changes pitch
speechSynthesis.speak(utterance);
```

**[2]改变速率**

如果您想要更改说话的速率，您可以降低或提高速率。(基本上就是说话人说话的快慢。)默认情况下，比率的值为 1。可接受的范围在 0.1 到 10 之间。

这里有一个例子:

```
let utterance = new SpeechSynthesisUtterance("Hello World");
utterance.rate= 4; //changes pitch
speechSynthesis.speak(utterance);
```

**【3】改变音量**

如果你想改变讲话的音量，你可以降低或提高它。默认情况下，音量值为 1。可接受的范围在 0 到 1 之间。

这里有一个例子:

```
let utterance = new SpeechSynthesisUtterance("Hello World");
utterance.volume= 0.4; //changes pitch
speechSynthesis.speak(utterance);
```

**【4】改变声音**

如果你想改变说话者的声音，你可以改变它。该界面提供了一系列声音。您可以使用`speechSynthesis.getVoices()`来检索这个声音数组，其中`getVoices()`是`speechSynthesis` 接口的一个方法。

这里有一个例子:

```
let utterance = new SpeechSynthesisUtterance("Hello World");
let voicesArray = speechSynthesis.getVoices();
utterance.voice = voicesArray[2];
speechSynthesis.speak(utterance);
```

如果您使用 CodePen 来测试这些不同的声音，您可能不会马上注意到声音的变化。确保你保存了密码笔(当你改变声音的时候),给它 10 到 20 秒来载入新的声音。我不知道 CodePen 为什么不立即修复语音，但事情就是这样。

这是笔。更改值。添加一些新代码。也许可以创建一个输入框，接收文本并将其转换为语音。玩弄它。看看会发生什么。

感谢您的阅读。很有趣！

如果你想学习如何使用其他[Web API](https://developer.mozilla.org/en-US/docs/Web/API)，给我一个关注。我们肯定会谈到语音到文本的转换，并获得用户的位置。几个月前，我在我的[天气应用](https://github.com/kyledeguzmanx/fDev-website-WeatherAppV1)中使用了 Web API 的地理定位 API。我应该做一个演练，或者一个改进的第二个版本？

有很多有趣的东西可以学。

感谢您的阅读。祝你愉快。继续编码！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*