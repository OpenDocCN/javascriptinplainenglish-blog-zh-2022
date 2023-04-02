# 如何在 JavaScript 中实现链表

> 原文：<https://javascript.plainenglish.io/how-to-implement-linkedlist-in-js-64bdc855215c?source=collection_archive---------7----------------------->

## JavaScript 链表实用指南

在这篇文章中，我们将会看到如何在 javascript 中实现链表及其各种操作。

![](img/9d8ce9385ef72de2be7ab539d916ff3e.png)

*注:*我选择了 Javascript 语言(我的最爱)来实现，语言在这里只是一个媒介，我们可以用任何编程语言来实现。关键思想是底层算法将始终保持不变。

在我们深入到编码部分之前，让我们从链表的定义开始。

# 什么是链表？

Def 1 —

链表是一种线性数据结构，其中元素被视为存储数据的节点和指向下一个节点(即元素)的指针。

Def 2 —

链表是一种线性数据结构，其中的元素不存储在连续的内存位置。

连续内存分配提供随机访问，即直接访问。由于数组元素是以这种方式存储的，所以访问任何元素都要花费恒定的时间，即 O(1)，而对于链表来说，要访问任何元素，我们必须跟随指针，所以这是一个顺序访问，需要 O(n)时间。

## 数组与链表

1.  访问第 I 个元素→数组 O(1) |链表 O(n)
2.  插入和删除→数组 O(n) |链表 O(1) —对于双向链表
3.  大小→数组—固定|链接列表—动态

# 链表操作

1.  横越
2.  链表的大小
3.  插入
4.  删除
5.  搜索

# 用 Javascript 实现链表

让我们为节点定义构造函数，也就是链表的元素

```
function Node(data) {
    this.data = data;
    this.next = null;
}
```

现在，我们可以定义 LinkedList 构造函数—

```
function LinkedList() {}
```

让我们在链表的原型中添加一个 **create** 函数，它将接受一个元素数组并创建链表。

```
LinkedList.prototype.create = function (arr) {
    let head = new Node(arr[0]);
    let temp = head; for (let i = 1; i < arr.length; i++) {
        temp.next = new Node(arr[i]);
        temp = temp.next;
    } // returning head of the linked list
    return head;
}
```

就这样，LinkedList 创建完毕😊

让我们实现每个基本操作。

## 遍历链表

从头节点开始，遍历到列表的末尾。

```
LinkedList.prototype.traverse = function (head) {
    let temp = head; while (temp != null) {
        console.log(temp.data);
        temp = temp.next;
    }
}
```

TC: O(n)

## 链表的大小

返回链表中所有元素的计数。

```
LinkedList.prototype.size = function (head) {
    let temp = head;
    let count = 0; while (temp != null) {
        count++;
        temp = temp.next;
    }

    return count;
}
```

TC: O(n)

## 在链表中插入

在链表中第 k 个索引处插入元素，并返回更新后的头

```
LinkedList.prototype.insert = function (head, k, elem) {

    let size = this.size(head);    

    // case 1\. if index k is not valid
    if (k < 0 || k > size) {
        return head;
    } let newNode = new Node(elem); // case 2\. insert at beginning
    if (k === 0) {
        newNode.next = head;
        return newNode;
    } // case 3\. insert at kth node
    let temp = head;

    for (let i = 0; i < k; i++) {
        temp = temp.next;
    }

    newNode.next = temp.next;
    temp.next = newNode;

    return head;
}
```

TC: O(n)

## 链表中的删除

从链表中删除第 k 个索引元素，并返回更新后的头

```
LinkedList.prototype.delete = function (head, k) {

    let size = this.size(head);    

    // case 1\. if index k is not valid
    if (k < 0 || k > size) {
        return head;
    } // case 2\. deletion at the beginning
    let temp = head; if (k === 0) {
        temp = head.next;
        head.next = null; return temp;
    } // case 3\. delete kth node
    temp = head;

    for (let i = 0; i < k; i++) {
        temp = temp.next;
    } let cur = temp.next; // this element would be deleted
    temp.next = temp.next.next; // or cur.next (both are fine)
    cur.next = null;

    return head;
}
```

TC: O(n)

## 在链接列表中搜索

给定链表的头和一个元素，在列表中搜索该元素。

```
LinkedList.prototype.search = function (head, elem) {
    let temp = head;
    let isFound = false; while (temp != null) {

        if (temp.data === elem) {
            isFound = true;
            break;
        }

        temp = temp.next;
    }

    return isFound;
}
```

TC: O(n)

# 结论

现在，您应该尝试自己创建 LinkedList 并实现每个操作。

之后，请尝试以下问题-

1.  反转链表
2.  找到链表的中间
3.  查找循环是否出现在链表中

希望你喜欢这篇文章，请分享给你的朋友。并访问 weekendtutorial.com 获得更多这样的文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***