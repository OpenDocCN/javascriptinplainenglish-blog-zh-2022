# “您”如何使用 JavaScript 制作一个简单的文本-语音转换器

> 原文：<https://javascript.plainenglish.io/how-you-can-make-a-simple-text-to-speech-converter-using-javascript-750350237dab?source=collection_archive---------9----------------------->

## 这里有一个使用 JavaScript 制作语音到文本转换器的简单方法

![](img/56f6fbf562f5299685483ffe87d0fcbf.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

每一个业余 JavaScript 程序员的初学者一定都想过制作一个文本到语音或语音到文本的转换器，但由于没有足够的知识或自己尝试而无法实现。所以在这篇文章中，我将教你做一个文本到语音的转换器，还有一个额外的提示，永远不要害怕在网上搜索那些你在编程中没有想到的东西，因为害怕感到羞愧

所以，事不宜迟，让我们来了解一下这个简单而又神奇的项目，它一定会给你的投资组合带来提升。

# 基础知识:

有一个为语音和文本功能制作的 web API。在这个 API 中，有一个`speechSynthesisUtterance()`函数用于为文本到语音转换提供一些选项，例如文本、语言、语音等，而`speechSynthesis()`函数用于执行关于文本到语音转换的各种功能，如朗读或获取语音等。

# 1.制作布局:

第一步是做一个布局。该布局必须包含一个用 HTML 中的`textarea`标签制作的文本框和一个开始演讲的按钮。给`textarea`和按钮一个 id。看下面这支笔来看我的布局。

# 2.编写 JavaScript:

第二步，写 JavaScript。首先，使用`document.getElementById("")`方法创建一个变量来保存`textarea`标签，在我的例子中，变量是`txt`。然后通过`new speechSynthesisUtterance()`方法创建一个新变量来存储`speechSynthesisUtterance()`，在我的例子中，变量是`speech`。然后使用`.lang = "en-US"`和您用来存储`speechSynthesisUtterance()`的变量来设置`speechSynthesisUtterance()`的语言，如第 3 行所示。

然后创建一个空数组，将其命名为 voices(您可以选择任何名称，但 voices 是最容易混淆的一个)。

*注意:-在全局范围内(任何函数之外)创建上述所有变量*

然后创建一个函数，使用`windows.speechSynthesis.onvoiceschanged = () => {}`在浏览器上获得可用的声音，并在花括号({ })内初始化`window.speechSynthesis.getVoices()`为声音。这将在浏览器加载时获取可用的声音。之后，通过将`.voice = voices[0]`添加到您用来存储`speechSynthesisUtterance()`的变量中，将`speechSynthesisUtterance()`的声音设置为“声音”数组中的第一个声音。

现在，最后一个函数实际朗读您在文本框中输入的文本。因此，创建一个函数，在该函数中，首先通过`variable_name_for_speechSynthesisUtterance().text = variable_name_for_textarea.value`将`speechSynthesisUtterance()`的文本设置为文本框的值，其中`variable_name_for_speechSynthesisUtterance`是用于存储`speechSynthesisUtterance()`的变量，而`variable_name_for_textarea`是用于存储`textarea`的变量。然后在那之后写`window.speechSynthesis.speak(variable_name_for_speechSynthesisUtterance()`，这里`variable_name_for_speechSynthesisUtterance`是你用来存储`speechSynthesisUtterance()`的变量，在我的例子中是`speech`。

现在，最后一步只是将函数名添加到按钮的`onclick`属性中，这样当它被点击时，文本框中的文本就会被读出。

这是你的文本-语音转换器。希望你喜欢它，它有助于提高你的投资组合，并随时给我建议，为进一步的文章。

再见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***