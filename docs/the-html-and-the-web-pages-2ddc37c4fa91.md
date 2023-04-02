# 你明白你在网页上看到的是什么吗？

> 原文：<https://javascript.plainenglish.io/the-html-and-the-web-pages-2ddc37c4fa91?source=collection_archive---------14----------------------->

## HTML 和网页——详细介绍。

![](img/1406c31677eba6c1981a007c3e73ded9.png)

Image By [James Osborne](https://pixabay.com/users/jamesmarkosborne-1640589/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1076533)

在我之前的文章中，[静态基础](https://blog.sapinder.dev/articles/web-development-the-static-fundamentals)和[动态 web](https://blog.sapinder.dev/articles/the-dynamic-web) ，我对 Web 开发领域做了一个全面的介绍，但是在接下来的两篇文章中，我们将对单个 Web 技术进行深入的基础研究。你准备好上路了吗？🚍这里是我们的第一站——***HTML***。

首先， *HTML 代表* ***超文本标记语言*** *，它是* ***而不是*** *一种编程语言。(哎呀…引发了争论🤦。首先，我们应该了解标记语言到底是什么。*

> [标记语言](https://en.wikipedia.org/wiki/Markup_language)是一种对文档进行编码的方式，它与文本一起包含标签或标记，这些标签或标记包含关于文本结构或其表示的附加信息。

简单来说，一种标记语言是用来以特定的结构呈现某一段数据的；可能是文字、图片、表格等。它不能用来对任何任务进行编程，这与编程语言必须具备的能力相反。HTML、XML、SVG 都是标记语言的例子。

现在回到 HTML，你在网页上阅读的文本不仅仅是纯文本，而是包含了大量关于文本的信息，这些信息告诉你文本的结构，以及它应该如何呈现。以下面的句子为例-

**我的名字是*萨宾德·辛格*。我是一名*内容创作者*。**

上面这句话的 HTML 代码是-

```
<b>My name is <i>Sapinder Singh</i>. I’m a <i>content creator</i>.</b>
```

如您所见，标签`<b>`(粗体)和`<i>`(斜体)有它们自己的方式来呈现它们所保存的数据。再考虑一个例子——
**“我用** [**VS 代码**](https://code.visualstudio.com/) **进行编码。”**

该文本包含一个 ***链接*** 到另一个网页，您可以通过点击突出显示的文本导航到该网页。这就是 HTML 中“超文本”的基本含义。[超文本](https://en.wikipedia.org/wiki/Hypertext)是任何包含对其他文本的引用的文本，可以通过与[超链接](https://en.wikipedia.org/wiki/Hyperlink)(在本例中是“VS 代码”)的交互来访问。本质上，这就是我们如何从一个网页跳到另一个网页。

# HTML 的语法概述

HTML 是网页的组成部分。它用不同的标签标识不同类型的文本和媒体，其中每个标签都在一对 ***开始*** 和 ***结束*** 标签中。例如，如果我们想写一段文字，我们可以像在`<p>`中那样打开`p`标签；插入文本；然后像在`</p>`中那样关闭标签。然后我们为每个标签设置了 ***属性*** 。

一个[属性](https://developer.mozilla.org/en-US/docs/Glossary/Attribute)只是一个标签的属性，它保存了某种类型的值。我们以`name="value"`的形式定义一个属性；例如，看看下面的代码片段，它定义了一个名为“VS Code”的超链接。标签`a` (anchor)用于定义一个超链接，它需要属性`href`指向一个 URL。

```
<a *href*="https://code.visualstudio.com">VS Code</a>
```

现在，有一些标签不需要关闭，这些被称为*自关闭*标签。我们不提供任何值，只是给这些标签提供了属性。自结束标签最基本的例子是所有 HTML5 文档必须以其开头的`<!Doctype html>`。它告诉浏览器遵循最相关的规范来呈现页面。你可以在 MDN 的[这个](https://developer.mozilla.org/en-US/docs/Glossary/Doctype)页面上找到一个关于 Doctype 的简短的&非常好的解释。尽管如此，HTML 文档中的所有内容都放在`html`标签中；这就是为什么它被称为**网页的根元素**。这个`html`标签由两部分组成- `head`和`body`。

```
<!Doctype html><html> <head></head> <body></body></html>
```

# 头

网页的`head`对用户来说不是直接可见的，因为它包含不被用户读取而是被浏览器读取的信息。它包含以下信息:

*   用于浏览器标题栏和搜索引擎优化的页面标题。
*   用于设计网页样式的样式。这些样式是用 CSS 编写的。
*   用于向网页添加可执行代码的脚本。脚本的唯一目的是处理网页上的用户交互。
*   用于附加信息的其他`meta`标签，例如[字符集](https://developer.mozilla.org/en-US/docs/Glossary/character_set)、[收藏夹图标](https://www.seoptimer.com/blog/what-is-a-favicon/)，以及其他类型的[元数据](https://developer.mozilla.org/en-US/docs/Glossary/Metadata)。

这里有一个我们通常在`head`标签中看到的例子

```
<head>*<!-- defines the character set of the web page -->*<meta *name*="charset" *content*="UTF-8">*<!-- defines the title of the web page -->*<title>The Theory Of HTML</title>*<!-- links the styles.css file to the web page -->*<link *href*="./styles.css" *rel*="stylesheet" *type*="text/css">*<!-- links the fonts from Google Fonts -->*<link*href*="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,600;0,700;0,800;1,600&display=swap"*rel*="stylesheet preload">*<!-- links the script.js file to the web page -->*<script *src*="./script.js"></script></head>
```

# 身体

`body`标签代表网页的可见部分。您在网页上阅读、看到或与之交互的任何内容都放在该网页的正文中。每种类型的内容由特定的标签表示；一些常见的标签是:

*   **p** —代表一段文字。
*   **img** —代表一幅图像。它需要包含图像路径的`src`属性。
*   **节** —代表页面的一个节。
*   **h1 至 h6** —代表一个区段的**航向级别**。可接受的最小航向级别是`<h6>`。
*   **按钮** —代表一个按钮。
*   **表单** —代表提交某些信息的表单。
*   **输入** —代表一个输入字段。根据`type`属性的值，它可以接受不同类型的输入。

你可以在 MDN 的 [HTML 参考页面](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)上阅读更多关于不同种类 HTML 元素的内容。

> **有趣的事实** 如果你省略、拼错或放错了 HTML 中的任何标签，浏览器就会悄悄地呈现布局不正确或不完整的页面。与编程语言不同， **HTML 不会抛出任何错误；因此证明了它只是一种标记语言。😉**

# 网页是如何呈现的

好了，现在你知道我们如何写 HTML 了；但是您还必须知道网页实际上是如何与链接到 HTML 文件的源代码一起呈现的。因此，一旦客户端浏览器收到 HTML 文件，它就开始创建所谓的[文档对象模型](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)。DOM 是一种类似倒树的对象模型，它的唯一目的是在内存中表示 HTML 文档，并使浏览器的 JavaScript 引擎能够理解它。这棵树的根是`html`元素，它分支成`head`和`body`，它们进一步分支成它们的子元素，以此类推。

> DOM 表示一个带有逻辑树的文档。树的每个分支都以一个节点结束，每个节点都包含对象。DOM 方法允许对树进行编程访问。使用它们，您可以更改文档的结构、样式或内容。
> - **MDN**

在构建 DOM 树时，浏览器会遇到几个在文档的`head`中定义的链接资源。考虑到我在 [head](https://blog.sapinder.dev/articles/the-html-and-the-web-pages/#head) 部分提供的片段，接下来会发生以下情况:

*   当它遇到*的`link`时。/styles.css* 文件，它暂停解析文档；向服务器请求文件；分析样式；并继续该过程。
*   然后遇到字体的`link`；同样，它首先请求字体；解析它们；并继续该过程。
*   最后，它会遇到`script`标签，并根据所提供的属性下载和执行该标签。(此处阅读更多)

一旦浏览器完成了对文档和样式的解析，它就将它们组合成一个 ***渲染树*** ，并计算出网页的布局。然后最后 ***绘制*** 文档，我们就能在浏览器窗口看到网页了。所有这些过程被称为关键渲染路径。如果想了解更多，可以阅读 MDN 的[本指南](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)。

# 包扎

所以那都是朋友！我希望你发现这个指南有助于加深你对 HTML 和网页的了解！如果你喜欢，一定要 ***关注我*** ，这样你就不会错过我以后的任何帖子了！你也可以在 [Twitter](https://twitter.com/sapinder_dev) 、 [Github](https://github.com/sapinder-pal) 和 [LinkedIn](https://www.linkedin.com/in/sapinder-singh/) 上查看我。

下一集再见！😉

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和谐***](https://discord.gg/GtDtUAvyhW) ***。******