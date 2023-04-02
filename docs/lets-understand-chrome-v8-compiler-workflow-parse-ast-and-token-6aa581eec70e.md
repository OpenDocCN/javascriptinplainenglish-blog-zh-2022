# 让我们来理解 Chrome V8:编译器工作流:解析、AST 和令牌

> 原文：<https://javascript.plainenglish.io/lets-understand-chrome-v8-compiler-workflow-parse-ast-and-token-6aa581eec70e?source=collection_archive---------7----------------------->

## 第 23 章:生成 AST 的工作流程

![](img/2229cb027639f57877eb360bf75cd927.png)

*欢迎阅读* [*其他章节让我们来了解一下 Chrome V8*](https://medium.com/@huidou)

在本文中，我将讨论 Parse、AST 和 Token 是如何协同工作的，并引导您完成编译以及观察和查看细节。具体来说，您将看到如何扫描标记，以及 Parse 如何使用标记来生成 AST 树。

# **1。Parse_Info**

下面是 Parse_Info 类。它是解析器的内核类，管理 JavaScript 源代码和 AST 树。简单地说，解析器的输入是 JavaScript 代码，输出是 AST 树。但是请注意，从 V8 加载 JavaScript 源代码的那一刻起，代码就已经被编码为 UTF-16 了。

让我们进入 Parse_Info。

在上面的代码中，第 5 行是 AST 工厂方法；第 13 行文字返回 AST 树；第 17 行 flags_ 显示了函数没有被优化的原因；第 33 行 literal_ 负责保存完整的 AST 树。正如我提到的，AST 是解析器的一个输出，所以如果您想详细查看解析器的工作流程，您只需调试它并继续查看成员变量 literal_，通过这种方式，您将看到 AST 的生成以及工厂方法是如何被调用的。

# **2。装配树**

正如我上面提到的，变量 literal_ 代表一个 AST 树，它的声明类是 FunctionLiteral。

我要强调的是，AST 粒度是一个函数，换句话说，一个 JavaScript 函数只对应一棵 AST 树。在上面的代码中，第 26 行成员变量 body_ 保存了 AST 正文，如果您对细节有疑问，请浏览正文。第 4–15 行将语言模式设置为严格或宽松。

再来看看第 18 行 FunctionKind。

您应该看到函数种类不是 JavaScript 书中的类型，因为函数种类只是表示编译器中的函数种类。有关详细信息，请参见编译器书籍。

# **3。AST 节点类型**

以下宏模板是不完整的节点类型列表。

在上面的代码中，参见第 34 行，它将所有的模板组织在一起，为作为编译器管道一部分的解析器中的 JavaScript 函数生成一个 AST 树。通过宏 AST_NODE_LIST，我们应该看到一个 AST 中有三个类型，每个类型又有更多的子类型。所有这些类型都对应于我们的 JavaScript 代码，并准确地表示语义。

# **4。令牌类型**

以下宏模板是不完整的标记列表。

令牌在扫描器中使用，扫描器是 V8 编译器的一部分，负责将 JavaScript 代码转换成令牌。举个简单的例子，见第 5 行，令牌类型是句点，对应 JavaScript 代码中的点，这意味着扫描器会把看到的每个点都转换成句点令牌。同样，第 10 行和第 12 行是轻括号和右括号，用于描述 JavaScript 代码中的`(`和`)`。所以在每一行，每一个以 T 开头的宏中，第一个参数是 token 类型，第二个是类型对应的词法，最后一个数字是 token 优先级，数字越小，token 越高，会越早转换。

# **5。有限状态自动化**

在大多数编译器中，词法分析器和语法分析器使用 FSA(有限状态自动化)来分析源代码。在 V8 中，它使用 switch-case 来实现 FSA，让我们看看 lexer FSA，即令牌扫描器。

ScanSingleToken()负责生成令牌。在第 8–40 行中，每个案例都是一个令牌。

下面的代码是解析器 FSA，它使用令牌并为 AST 树生成节点。

最后，我认为 FSA 是编译器的一个重要基础，值得更深入地研究。

*好了，这部分就到此为止了。下次再见，保重！*

如果你有任何问题，请联系我。**微信** : qq9123013 **邮箱**:[v8blink@outlook.com](mailto:v8blink@outlook.com)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***