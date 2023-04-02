# JavaScript:集合数据结构

> 原文：<https://javascript.plainenglish.io/javascript-the-set-data-structure-1763c16e614a?source=collection_archive---------9----------------------->

## 了解 JavaScript 中的集合数据结构以及它与数组的不同之处。

![](img/6f744fb7b98ebb83308618eec03c141c.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

set 数据结构是 JavaScript 语言中相对较新的内容。是在 2015 年发布的 ES6 中加入的。尽管 set 数据结构相对年轻，但由于它的许多优点，它已经在开发人员中流行起来。

在这篇博文中，我们将讨论什么是集合，它们是如何工作的，以及如何在自己的项目中使用它们！

## 什么是集合？

集合是唯一值的集合。也就是说，集合项在集合中只能出现一次。这与数组相反，数组可能包含重复值。因为集合只允许唯一的值，所以它们通常用于从数组中删除重复值。

## 集合是如何工作的？

使用 JavaScript Set 对象设置工作。此对象提供了几种处理集合的方法，例如添加和移除项、检查集合中是否存在项以及清除集合。让我们看一些代码示例，看看这在实践中是如何工作的。

## 向器械包添加物品

可以使用`add()`方法将物品添加到器械包中。此方法将一个项作为参数，并将其添加到集合中。如果该项目已经存在于集合中，则不会再次添加。

下面的代码示例创建一个新的 Set 对象，并向其中添加一些项:

如您所见，`add()`方法用于向集合中添加项目。在本例中，我们将字母“a”、“b”和“c”添加到集合中。字母“a”不会添加两次，因为该值已经在集合中。

## 检查集合中是否存在某个项目

`has()`方法可以用来检查一个项目是否存在于集合中。此方法将一个项目作为参数，如果该项目存在于集合中，则返回 true，否则返回 false。

下面的代码示例创建一个新的 Set 对象，并向其中添加一些项:

在这个例子中，我们使用`has()`方法来检查集合中是否存在项目‘a’和‘d’。如您所见，集合中存在“a”(返回 true)，但“d”不存在(返回 false)。

![](img/ece7b616d59c95113eaf1a830a392b77.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 从集合中移除项目

使用`delete()`方法可以从器械包中移除物品。此方法将一个项作为参数，并将其从集合中移除。如果集合中不存在该项，此方法将返回 false。

下面的代码示例创建一个新的 Set 对象，并向其中添加一些项:

在这个例子中，我们使用`delete()`方法从集合中删除项目“b”。如您所见，在项目被移除后，只有“a”和“c”保留在集合中。

## 清除器械包

`clear(`)方法可用于移除集合中的所有项目。该方法不带任何参数，返回一个空集。

下面的代码示例创建一个新的 Set 对象，并向其中添加一些项:

如您所见，`clear()`方法从集合中移除了所有的项目，留下了一个空集。

## 集合与数组

正如我们之前提到的，集合只允许唯一值，而数组可以包含重复值。这是集合和数组的主要区别。但是，还需要注意其他一些差异:

*   集合是无序的，而数组是有序的。这意味着集合的项目没有特定的顺序，而数组有。
*   集合不能通过索引访问，而数组可以。这意味着您不能使用方括号符号来访问集合中的特定项，但是可以使用数组。

## 结论

集合数据结构是一个非常强大的工具，可以用于许多目的。我希望这篇文章能消除你对 JavaScript 集合的任何困惑！祝你的编码面试好运！

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*