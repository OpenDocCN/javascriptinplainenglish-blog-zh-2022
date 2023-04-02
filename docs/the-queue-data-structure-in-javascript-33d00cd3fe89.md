# JavaScript 中的队列数据结构

> 原文：<https://javascript.plainenglish.io/the-queue-data-structure-in-javascript-33d00cd3fe89?source=collection_archive---------10----------------------->

## 定义队列数据结构，它的实际应用，如何用 JavaScript 创建队列，队列的时间复杂度。

![](img/ef1cb82745b169d7d2de4c0cc375b4ca.png)

Photo by [Melanie Pongratz](https://unsplash.com/es/@melanie_sophie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

队列数据结构是计算机科学中最常用的结构之一。它简单、高效、易于理解。在本文中，我们将讨论什么是队列，它是如何工作的，以及它的一些应用。我们还将提供如何用 JavaScript 创建队列的例子。

## 什么是队列？

队列是一种允许以先进先出(FIFO)方式存储数据的数据结构。也就是说，添加到队列中的第一个元素将是第一个被移除的元素。这与堆栈相反，堆栈是一种后进先出(LIFO)的数据结构。

## 队列为什么有用

计算机系统中经常使用队列来保存需要以特定顺序处理的数据。例如，当一个新任务进入系统时，它通常被添加到队列的末尾。然后按照接收的顺序一次处理一个任务。这确保了所有的任务以公平和有效的方式被处理。

## 队列的实际应用

队列有许多应用。展示其多功能性和重要性的一些常见应用包括:

*   键盘序列:当你在键盘上打字时，字符被存储在一个队列中，直到它们可以被计算机处理。
*   打印机:当您将打印作业发送到打印机时，它通常会被添加到队列的末尾。然后按照接收的顺序处理打印作业。
*   任务调度:当新任务进入系统时，它们被添加到队列中。然后，任务按照接收的顺序进行处理。这确保了所有的任务以公平和有效的方式被处理。

![](img/5d53049093cc3c3a16c4417aaf5511e5.png)

Photo by [Avel Chuklanov](https://unsplash.com/es/@chuklanov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 创建队列并添加到队列中

在 JavaScript 中，我们可以使用数组创建队列。以下示例创建一个包含三个元素的队列:

向队列添加元素通常是使用`push()` 方法完成的。方法将一个元素添加到数组的末尾。在上面的例子中，我们向队列中添加了三个元素。

## 从队列中移除

在 JavaScript 中，我们可以使用`shift()`方法从队列中移除元素。方法从数组中移除第一个元素。在下面的示例中，我们从队列中删除了第一个元素，并将其存储在一个变量中:

在上面的例子中，队列是通过分别按“第一”、“第二”和“第三”的顺序创建的。根据队列的先进先出原则，“first”是从队列中移除的第一个元素。我们通过利用`shift()`方法，从队列的开始删除‘第一个’来完成这个任务。

![](img/fcb259b9ceaa502fa6935609315ba415.png)

Photo by [Hatice Yardım](https://unsplash.com/@haticehuma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 时间复杂度

通常，使用队列的好处之一是添加和删除元素的时间复杂度是恒定的。也就是说，无论队列中有多少个元素，添加或删除一个元素都需要相同的时间，通常为 O(1)。

然而，在 JavaScript 中，没有内置的队列数据结构，我们必须用数组来复制队列的功能。我们用来向队列中添加元素的`push()`方法的时间复杂度为 O(1)，而我们用来从队列中删除元素的`shift()`方法的时间复杂度为 O(n)。这是因为当我们将一个元素移出数组的开头时，数组中的所有其他元素都必须移动一个位置。

## 结论

在本文中，我们讨论了队列数据结构及其一些实际应用。我们还展示了如何用 JavaScript 创建队列，并讨论了 JavaScript 中队列的时间复杂度。队列简单、高效、易于理解，使其成为许多应用程序的最佳选择。

我希望这篇文章澄清了任何困惑。祝你的编码面试好运！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****