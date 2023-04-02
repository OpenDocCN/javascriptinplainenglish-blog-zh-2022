# 数据结构和算法:生成括号

> 原文：<https://javascript.plainenglish.io/data-structures-and-algorithms-generate-parentheses-768e3a77a22c?source=collection_archive---------0----------------------->

## 写一个生成括号的算法——常见的面试问题。

![](img/19e9d30f77f57a8f419feff3bbe8e56d.png)

Photo by [Chris Ried](https://unsplash.com/@cdr6934?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为工作面试学习数据结构和算法问题可能很难。这些问题都是废话，所以要熟悉哪种类型似乎是随机的。我在不同的工作面试中多次遇到过这样的问题:

给定`n`对括号，编写一个函数来*生成所有格式良好的括号的组合。*

例如，输入 3 将导致:

[“((()))”, “(()())”, “(())()”, “()(())”, “()()()”]

输入为 3 时，“格式良好”意味着每个排列将有三个左“(”和三个右“)”括号。让我们看看如何解决这个问题。

首先，让我们看看一些约束条件。我们已经确定了什么是格式良好的括号。我们也知道右括号不应该出现在左括号之前。左括号和右括号的数量应该相等，并且它们的数量不应大于`n`。

考虑到这些限制，让我们创建一个基本案例，其中的条件大致描绘了需要实现的目标。

*   需要存储有效的排列。因此，需要一个数组。我们称它为`result`。
*   我们的函数应该检查创建的左括号和右括号的数量是否等于`n`。为了保持跟踪，我们将在每次使用左括号和右括号时增加一个计数。如果等于`n`，将该排列添加到数组中。如果没有，则添加另一个左括号并增加其计数。然后检查左括号的数量是否大于右括号的数量。如果是，我们将添加另一个右括号并增加它的计数。
*   我们需要确保在`result`数组中没有任何重复的排列

看看上面的大纲，重复和迭代的数量是使用递归的一个很好的例子。虽然我们可以从字面上找到每一个排列，然后过滤掉任何重复的，这将是低效的。我们将采用以下方法来避免重复并仅生成有效的排列:

1.  如果左括号的数量小于`n`，则递归调用函数，同时增加一个左括号。
2.  如果右括号的数量少于左括号，则递归调用该函数，同时添加一个右括号。

我们实际上将创建两个函数。一个递归函数将产生所有的排列。它将接受`result`数组、括号字符串、括号计数和输入`n`。另一个函数将输入作为参数，创建`result`数组，对递归函数进行初始调用以收集所有排列并返回数组。

让我们按照这个输入为 2 的代码。

`genParentheses(2)`

创建了`result`数组，然后调用递归函数。

`getParens(result, "", 0, 0, 2)`

现在关注函数调用的这一部分，因为这是理解其工作原理的关键:

在本例中，`n`为 2，if 语句实际上创建了两个分支。

**分支 1**

*   检查`open`的值，当前为 0，递归调用`genParens`。
*   "("被添加到字符串`s`并且`open`增加到 1。
*   再次检查`open`的值，该值现在为 1。对`genParens`进行另一次递归调用。
*   "("被添加到字符串`s`中，现在等于`"(("`。`open`的值增加到 2。
*   `open`的值现在与`n`相同，不再触发第一个 if 语句。
*   转到第二个 if 语句，`close`当前处于小于`open`的 0，因此对`getParens`进行递归调用。
*   ”)加到`s`上，现在等于`"(()"`。`close` 现在增加到 1。
*   `close`为 1，仍然小于`open`，因此再次调用`getParens`。
*   ”)加到`s`上，现在等于`"(())"`，而`close`增加到 2。
*   `open`和`close`现在都等于`n`。字符串`s`被添加到数组`result`中。

**分支 2**

*   在对`getParens`的第一次递归调用中，当`s`当前等于`"("`时，`close`的值小于`open`，因此它递归并开始第二个分支。
*   ”)加到`s`，现在等于`"()"`，`close`现在等于 1。
*   `open`此时为 1，因此它递归，将“(”添加到`s`，并增加到 2。
*   `close`现在再次小于`open`，所以它递归，将“)”加到`s`，并且也增加到 2。
*   `s`现为`"()()"`。`open`和`close`都等于`n`，所以`s`被添加到数组`result`中。

这两个分支现在都满足了停止递归的条件。数组`result`被返回，看起来像这样:`["(())", "()()"]`

输入值越高，获得所有不同排列的分支就越多。最终结果返回格式良好且唯一的括号组合。

希望这有所帮助。感谢阅读。下次见！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**