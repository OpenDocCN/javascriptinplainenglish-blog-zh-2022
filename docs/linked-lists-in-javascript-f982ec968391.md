# JavaScript 中的链表

> 原文：<https://javascript.plainenglish.io/linked-lists-in-javascript-f982ec968391?source=collection_archive---------8----------------------->

## 如何创建链表和可以在其上使用的通用算法。

![](img/5d5d56e877ad7602838b0e7112eb5acb.png)

Photo by [Karine Avetisyan](https://unsplash.com/@kar111?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

链表是一种用于以线性方式存储数据的数据结构。这意味着数据是一个接一个地存储的，每个项目都链接到列表中的下一个项目。这对于存储数据非常有用，尤其是当您需要以特定的顺序访问数据时。在这篇博文中，我们将讨论如何创建链表以及可以在其上使用的通用算法。

## 为什么链表是有用的

链表在插入和删除数据时非常有效。这是因为列表中的每一项都只与下一项相连，所以在插入或删除内容时，不需要重新排列列表中的任何其他项。这使得链表非常快速和灵活。

链表的另一个优点是它们很容易扩展。如果您需要向列表中添加更多的项目，您可以简单地将它们添加到列表的末尾，而不必担心更改列表中的任何其他项目。

## 创建链接列表

创建链表的第一步是创建一个节点类。这将用于存储列表中每个项目的数据。节点类应该有两个属性:data 和 next。Data 将用于存储节点的实际数据，next 将用于存储列表中的下一个节点。

```
class Node { constructor(data) { this.data = data; this.next = null; }}
```

接下来，我们需要创建一个 LinkedList 类。这将用于存储和管理我们的链表。LinkedList 类应该有两个属性:head 和 tail。头部将用于存储列表中的第一个节点，尾部将用于存储列表中的最后一个节点。

```
class LinkedList { constructor() { this.head = null; this.tail = null; }}
```

现在我们有了 Node 和 LinkedList 类，我们可以开始创建链表了！为此，我们将首先创建 LinkedList 类的一个新实例。然后，我们将创建一个新的节点实例，并将其设置为列表的头部。

```
const list = new LinkedList();const node = new Node(12);list.head = node;
```

## 添加到链表的头部

现在我们有了链表，我们可以在链表的头部添加一个节点。为此，我们将创建一个新的节点实例，并将其 next 属性设置为列表的当前头部。这样，我们的节点将指向链表的当前头部。然后，我们将设置列表的头部作为我们的新节点。

```
function addToHead(val) { const node = new Node(val); node.next = list.head; list.head = node;}
```

## 添加到链表的尾部

我们还可以在链表的尾部添加一个节点。为此，我们将创建一个新的节点实例，并将其 next 属性设置为 null。然后，我们将设置列表的尾部作为我们的新节点。

```
function addToTail(val){ let currentTail = list.tail; const node = new Node(val); node.next = null; currentTail.next = node list.tail = node;}
```

![](img/d41e7e64868b7748d6e6a285a5f96086.png)

Photo by [Max Duzij](https://unsplash.com/es/@max_duz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 删除链表中的节点

如果我们想从链表中删除一个节点，我们可以简单地将前一个节点的 next 属性设置为我们要删除的节点之后的下一个节点。

```
function deleteNode(target) { let currentNode = list.head; let prevNode = new Node(); prevNode.next = list.head; while (currentNode) { if (currentNode.data === target) { prevNode.next = currentNode.next; currentNode.next = null; return; } else { prevNode = currentNode; currentNode = currentNode.next; } }} 
```

## 遍历一个链表

现在我们有了链表，我们可以把它打印出来看看它是什么样子的！为此，我们将创建一个函数，它接收一个链表并打印出列表中每个节点的所有数据。

```
function printLinkedList(list) { let current = list.head; while (current) { console.log(current.data); current = current.next; }}printLinkedList(list);
```

## 反转链接列表

我们也可以反转链表。为此，我们将创建一个临时变量来保存当前节点的 next 属性。然后我们将把当前节点的 next 属性重新分配给前一个节点。然后我们将更新我们的变量。在算法的最后，我们之前的节点将成为新的头。

```
function reverseLinkedList(head) { let prev = null; let currentNode = head; while (currentNode) {
      let temp = currentNode.next; currentNode.next = prev; prev = currentNode; currentNode = temp;
  }

  return prev;
};
```

## 查找链表的中间

我们也可以在链表中找到中间的节点。为此，我们将创建两个指针:一个一次移动一个节点，另一个一次移动两个节点。然后我们将遍历列表，直到第二个指针到达列表的末尾。发生这种情况时，第一个指针将位于中间节点！

```
function findMid(list) { let slowPointer = list.head; let fastPointer = list.head; while (fastPointer && fastPointer.next) { slowPointer = slowPointer.next; fastPointer = fastPointer.next.next; } console.log(slowPointer.data);}
```

链表是在 JavaScript 中存储数据的一种很好的方式。它们易于创建和操作，并且比其他数据结构有更大的优势。我希望这篇文章已经澄清了你的任何困惑。祝你的编码面试好运！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*