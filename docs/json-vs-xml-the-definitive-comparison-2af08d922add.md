# JSON 与 XML:决定性的比较

> 原文：<https://javascript.plainenglish.io/json-vs-xml-the-definitive-comparison-2af08d922add?source=collection_archive---------16----------------------->

## JSON 和 XML 哪个更好——选择正确的数据传输格式

![](img/5dd40abcc756c59af8ba94fd96842d38.png)

Photo by [Joey Kyber](https://unsplash.com/@jtkyber1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您可能至少听说过一次 JSON 和 XML 这两种来回移动数据的不同方法。这些方法是不同的，我们将在本文中发现它们的优缺点。

读完这篇文章，你会知道什么是最好的，以及下次你需要一种格式来传输你的项目层中的数据时该选择什么。让我们开始吧。

# 快速解释

## JSON

从技术上讲，JSON 是一种文件格式，它喜欢使用易于阅读的测试来存储和传输包含属性-值对和其他数据结构(如数组等)的对象中的数据。

它用于存储从人的角度来看需要易于访问和阅读的信息。JSON 的意思是 JavaScript 对象符号，这意味着它与 JavaScript 中的对象具有相同的符号，这使它成为他们最喜欢的标准。的确如此。json 扩展。

样本:

```
{
  "student": [ 

     { 
        "id":"01", 
        "name": "Tom", 
        "lastname": "Price" 
     }, 

     { 
        "id":"02", 
        "name": "Nick", 
        "lastname": "Thameson" 
     } 
  ]   
}
```

## 可扩展标记语言

XML 是一种可扩展的标记语言，其语法类似于 HTML。它被设计用来存储数据，也是为了传输数据。它区分大小写，有严格的规则，允许您定义元素和定制语言。

XML 文件的基本单位是一个元素，它非常健壮。的确如此。xml 扩展。

样本:

```
<?xml version="1.0" encoding="UTF-8" ?>
<root>
	<student>
		<id>01</id>
		<name>Tom</name>
		<lastname>Price</lastname>
	</student>
	<student>
		<id>02</id>
		<name>Nick</name>
		<lastname>Thameson</lastname>
	</student>
</root>
```

# 主要特征

## JSON

*   JSON 非常容易使用。访问该结构中所有需要的数据非常容易。
*   JSON】不需要任何外部依赖。它有自己独立的简单规则。
*   **JSON 是免费和开源的。**
*   JSON 是 **performant** ，内存消耗低，适合大规模系统。
*   **JSON 对于每个人来说都很容易读懂**。

## 可扩展标记语言

*   XML 是灵活和可定制的。标签不是预定义的。
*   XML 适合于移动数据，而不是显示数据。在给定一些数据的情况下，这给了开发者更多的 UI/UX 设计的自由。
*   XML 是可扩展的。
*   对于人类来说，XML 代码非常容易阅读和编写。
*   它基于 HTML 规则，所以对大多数程序员来说是简单而直观的。

# 主要差异

虽然 JSON object 有类型，但是 XML 是无类型的，这也使 XML 更加灵活，但是在使用它的时候可靠性却有所下降。

几乎任何编程语言都可以通过代码直接访问 JSON 数据，而 XML 需要被解析。这可能需要编写更多的代码，从而降低程序的效率。

JSON 不太安全，而 XML 有一个完整的标准，可以确保比 JSON 更安全。

与 XML 文件相比，JSON 文件更容易编写和阅读，不管怎样，XML 文件都足够简单。

![](img/72432a6ca11794f2e51a791e690101c0.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JSON 不支持名称空间，而 XML 以一种非常有效的方式支持名称空间。这在某些代码片段重复出现的情况下会很方便，使 XML 结构更加清晰。

JSON 不支持编码，只支持 UTF-8 编码，而 XML 同时提供注释和各种编码格式。请注意，对于大多数任务，您不会注意到这种差异。

大多数浏览器都支持 JSON，而 XML 在这方面有一些问题。由于严格的规则，跨浏览器的 XML 解析可能相当困难。

在 JSON 中，更容易创建更多的嵌套对象和各种深度，这很有用，尤其是对于微服务基础设施。XML 不像 JSON 那样让嵌套对象变得简单明了。

# 优势

我们在文章中讨论了它们的一部分，但是本节和接下来的内容会让一切变得更加清晰。

## JSON

*   本机具有完整的浏览器支持
*   您可以在大多数语言中直接解析它
*   易于阅读和书写
*   所有主流框架和技术都支持和使用它，尤其是在后端(例如序列化器等等)。最后，它是最受欢迎的
*   由于低内存消耗，它是轻量级的和高性能的

## 可扩展标记语言

*   允许在本地创建给定的标签和数据结构
*   它可以很容易地从前端分离数据(原生 HTML)
*   它使得文档可以通过共享的规则在系统间传输，高效可靠
*   更安全

# 不足之处

## JSON

*   它没有名称空间支持
*   它是独立的，所以它没有开发工具支持

## 可扩展标记语言

*   需要被解析以被代码本身读取
*   它没有原生数据类型支持，这使得一切都不那么精确和流畅
*   XML 语法往往非常冗余，因此它消耗了大量的有用空间，并使程序变慢。

# 结论

最后，你可能会明白，它们都是很好的选择，有不同的好处和缺点，这与它们的本质有关。

所以，对每一个选项来说都没有最好的选择，这要看情况。

如果您的目标是性能、数据安全或者您正在使用 Javascript，请使用 JSON。

如果你想要更多的安全性，或者你需要更多的编码格式(我认为你不会)XML 是最好的选择。

总的来说，我在不同的案件中与他们都合作过。在我看来，JSON 是最好的选择，因为它更容易使用和解析，速度更快，冗余更少。它让一切都易于使用。

在每种编程语言中，都有一种方法可以将 JSON 与原生数据结构结合使用，比如 Javascript 中的对象、Python 中的字典等等。这使得它成为编码阶段简化的最合适的选择。

最后但同样重要的是，另一个重要的方面是受欢迎程度。JSON 更受欢迎，因此它在现实世界中有更多的用途，也得到社区更多的支持。事实上，该标准也是开源的。

所以，在我看来，无论如何你都应该选择它，但是 XML 也是一个非常有价值的选择。这是你的选择。

希望你喜欢这篇文章，如果你考虑鼓掌和订阅，或者点击这个链接来支持这个博客和整个平台:

[](https://medium.com/@mpossamaim/membership) [## 通过我的推荐链接加入 Medium-Matteo Possamai

### 阅读并支持 Matteo Possamai，你的贡献将会支持 Matteo…

medium.com](https://medium.com/@mpossamaim/membership) 

非常感谢。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***