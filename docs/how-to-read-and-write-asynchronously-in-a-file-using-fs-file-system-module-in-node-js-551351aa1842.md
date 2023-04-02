# 如何在 Node.js 中使用 FS(文件系统)模块读写(异步)文件

> 原文：<https://javascript.plainenglish.io/how-to-read-and-write-asynchronously-in-a-file-using-fs-file-system-module-in-node-js-551351aa1842?source=collection_archive---------7----------------------->

## 这比你想象的要简单

![](img/5df687501c532f24adfb234bf9a170b6.png)

Photo by [Ben Weber](https://unsplash.com/@benearlweber?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

网上关于 Node.js 和文件系统(fs)的文章足够多吗？

还是因为编程语言不断频繁进化，编程中的一些概念在互联网上变得很难找到？

最近，我想在我的 Windows 电脑上运行一个 Linux 环境。我很难在网上找到解决的方法。如果你正面临同样的挑战，这是我写的一篇文章。

现在，对于 Node.js 中的文件系统(fs)，我搜索了互联网，注意到关于如何在 Node.js 中使用 fs 读写文件的文章没有区分这些方法——readFile()和 readFileSync()、writeFile()和 writeFileSync()。

因此，这篇文章。

您将学习如何异步读写文件，以及如何使用 readFile()、readFileSync()、writeFile()和 writeFileSync()方法，包括它们之间的差异。

## readFile()和 readFileSync()的区别；writeFile()和 writeFileSync()

在 Node.js 中，readFile()和 readFileSync()是 fs 方法，可用于在不打开文件的情况下读取文件内容。然而，这两个 Node.js fs 方法之间存在差异。

当您希望运行同步操作并希望所有其他操作在完成之前都被阻止时，可以使用 readFileSync()方法。方法意味着一次只能读取一个文件，并且在读取完文件之前，不能同时读取和写入文件。

这意味着您不能同时异步执行多个操作。
readFile()fs 方法不同。您使用 fs 方法异步执行操作。用这种方法，可以一次读取一个文件和写入一个文件。

writeFile()和 writeFileSync() Node.js fs 方法也会发生同样的情况。

writeFile()方法允许您写入文件，在写入文件的同时，您还可以运行 readFile() fs 方法来读取文件的内容或一次做一些其他事情——异步地。

Node.js 作为一个运行时环境，从浏览器中脱颖而出的一个原因是它能够执行异步操作。

让我们看一些样本代码。

在开始之前，如果您还没有安装 Node.js，请在您的机器上安装它。每次你想运行一个代码时，先保存代码，然后用 Node 运行你的 JavaScript 文件，如下所示:

```
node index.js
```

## 如何使用 writeFileSync() Node.js fs 方法写入文件

首先，打开您的 VS 代码(或者您选择的其他 IDE)并创建一个文件夹。将文件夹命名为文本。在文件夹中，创建两个文件。将第一个文件命名为 index.js，将第二个文件命名为 text.txt。

在 index.js 中编写 JavaScript 代码，第二个文件将是您使用 Node.js writeFileSync()方法编写文本的位置。

它是这样工作的:

要使用 Node.js 写入文件，请在代码的第一行使用缩写为 fs 的文件系统模块。为了让 fs 工作，需要包含 require 关键字。

现在，您可以访问文件系统中的所有方法。

然后，将 fs 存储在一个变量中。这里我用了 fs(作为变量)— const fs。它会将文件系统模块中的所有方法存储在 fs 变量中。

请注意，除了 fs 之外，您还可以为变量指定一个不同的名称。第三行代码使用了 writeFileSync()方法。然后从根文件夹中跟踪要写入的 text.txt 文件的位置。/text/text.txt .圆点表示文件夹 text folder 和 text.txt 文件在同一个目录下。

接下来是你想在 text.txt 文件中写什么——你要不断尝试，直到你成功。

请注意，您可以将想要写入的内容存储在一个变量中，然后在 writeFileSync 中传递该变量，而不是像上面那样对 text.txt 文件中的内容进行硬编码，如下所示:

utf-8 有助于确保您的文本转换成英文字符，即使这些字符是英文字母。

## 如何使用 readFileSync() Node.js fs 方法读取文件

下面是如何使用 readFileSync() Node.js fs 方法读取文件。

readFileSync()遵循与 writeFileSync()方法相同的代码模式。

## 如何异步读取一个文件并写入另一个文件

使用 Node.js fs 模块，您可以读取一个文件的内容，并写入另一个文件，而不会互相阻塞。

创建另一个。txt 文件，并将其命名为 input.txt。

在 input.txt 文件中，写入—浏览。这是我对年轻时的自己反复说的话。

现在运行代码来读取 input.txt 文件中的内容，同时在 text.txt 文件中写入内容:

当计算机试图读写输入和文本文件时，您将首先看到显示在终端上的最后一行代码。然后，您将看到 text.txt 文件被读取，input.txt 文件被写入。

代码遵循 JavaScript 中的函数模式。它还使用了 if/else 语句。如果您不知道 JavaScript 语法，我建议您在深入学习 Node.js 之前先学习 JS。

此外，当您希望代码异步运行时，不能使用 readFileSync()或 writeFileSync() fs 方法。

**附言** *作家面临的挑战可能会让他们终生无法写作……久坐导致的慢性背痛、长时间盯着屏幕导致的眼睛问题、写作时手指窒息等等。如果你想继续得到这种类型的文章，你可以通过成为* [*媒体订户来支持我。每月 5 美元。你的一部分订阅费归我*](https://sabitololade.medium.com/subscribe) *。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*