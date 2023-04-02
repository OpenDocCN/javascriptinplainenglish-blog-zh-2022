# 使用 JavaScript 反转堆栈

> 原文：<https://javascript.plainenglish.io/reverse-stack-using-javascript-393592d96484?source=collection_archive---------22----------------------->

## 关于如何使用 JavaScript 反转堆栈的教程。

![](img/72de794832085b439159004cf8bcdf33.png)

先说栈的定义。

# 什么是堆栈？

堆栈是一种线性数据结构，其工作原理是**后进先出**(俗称 LIFO)。

如果你知道*递归*的话，程序控制必须深入(向下)并向上构建解决方案，栈是显而易见的选择。

堆栈最适用的其他问题:

*   检查括号是否平衡
*   使用堆栈反转数组
*   表达式计算

# 如何在 JavaScript 中创建堆栈？

堆栈数据结构支持以下原语操作:

*   推动(值)
*   流行()
*   peek()
*   is_empty()

让我们为栈定义对象原型，然后实现每个原语操作。

***注意:*** 栈可以用数组、队列、链表实现。为了简单起见，我们将使用数组来创建堆栈。

```
function Stack() {
  this.arr = []; // to store the stack data
  this.top = 0; // to point the top of the stack
}
```

# 推送(值):

push 函数接受参数“value ”,并将其插入堆栈的顶部。

```
Stack.prototype.push = function (value) {
  this.arr[this.top] = value; // store the value at the top
  this.top = this.top + 1; // increment top pointer
}
```

时间复杂度:O(1)
空间复杂度:O(1)

# Pop():

pop 在移除栈顶元素后返回它。

```
Stack.prototype.pop = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var topEl = this.arr[this.top - 1];

  this.top = this.top - 1;
  this.arr.pop();

  return topEl;
}
```

时间复杂度:O(1)
空间复杂度:O(1)

# peek():

peek 函数不从堆栈中删除数据，而是返回堆栈的顶部

```
Stack.prototype.peek = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  return this.arr[this.top - 1]; 

}
```

时间复杂度:O(1)
空间复杂度:O(1)

# is_empty():

如果堆栈为空，is_empty 函数返回 true，否则返回 false

```
Stack.prototype.is_empty = function () {
  return this.top === 0;
}
```

时间复杂度:O(1)
空间复杂度:O(1)

***注:*** 我们可以看到所有的图元操作都在花费恒定的时间。因此，如果我们从其他线性数据结构创建堆栈，那么我们必须确保原始操作也是常量时间。

让我们把所有的代码放在一起:

```
function Stack() {
  this.arr = [];
  this.top = 0;
}

Stack.prototype.push = function (val) {
  this.arr[this.top] = val;
  this.top = this.top + 1;
}

Stack.prototype.pop = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var topEl = this.arr[this.top - 1];

  this.top = this.top - 1;
  this.arr.pop();

  return topEl;
}

Stack.prototype.is_empty = function () {
  return this.top === 0;
}
```

# 怎么反叠？

## 方法 1 —修改原始堆栈

从堆栈中逐个弹出元素并存储在新字符串中，这个新字符串将是原字符串的反向。

让我们创建一个反转堆栈并返回反转字符串的反转函数。

```
Stack.prototype.reverse = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var revStr = '';

  while(!this.is_empty()) {
    revStr += this.pop();
  }

  return revStr;
}
```

时间复杂度:O(n) →处理完整的堆栈
空间复杂度:O(n) →存储字符串中的 n 项

## 方法 2 —保持原始堆栈不变

因为，在栈实现中，我们有栈`arr`的引用，它有栈数据。现在有了`top`指针，我们可以循环遍历`arr`，处理堆栈，存储反向字符串并返回。

```
Stack.prototype.reverseAlternate = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var revStr = '';

  for (var i = this.top - 1; i >= 0; i--) {
    revStr += this.arr[i];
  }

  return revStr;
}
```

时间复杂度:O(n) →处理驻留在`arr`
的栈数据空间复杂度:O(n) →存储字符串中的 n 项

将所有代码与一个示例结合在一起:

```
function Stack() {
  this.arr = [];
  this.top = 0;
}

Stack.prototype.push = function (val) {
  this.arr[this.top] = val;
  this.top = this.top + 1;
}

Stack.prototype.pop = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var topEl = this.arr[this.top - 1];

  this.top = this.top - 1;
  this.arr.pop();

  return topEl;
}

Stack.prototype.is_empty = function () {
  return this.top === 0;
}

Stack.prototype.reverse = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var revStr = '';

  for (var i = this.top - 1; i >= 0; i--) {
    revStr += this.arr[i];
  }

  return revStr;
}

Stack.prototype.reverseV1 = function () {
  if (this.is_empty()) {
    throw new Error("Underflow, stack is empty");
  }

  var revStr = '';

  while(!this.is_empty()) {
    revStr += this.pop();
  }

  return revStr;
}

var stack = new Stack();

stack.push('a');
stack.push('b');
stack.push('c');

console.log(stack.reverse()); // cba
console.log(stack.reverseV1()); // cba
```

## 方法 3—反转原始堆栈

需要明确的是，在 O(1)的空间复杂度下，反转栈是做不到的。

让我们深入了解以下有趣的场景-

如果要求在不使用除 stack 之外的其他线性数据结构的情况下反转原始堆栈。

用数组反转堆栈很简单，但是我们不允许使用它，但是，我们可以用 ***n*** 数量的堆栈来解决它但是不能用其他的线性数据结构。

例如

```
 stack1 = [1, 2, 3, 4, 5], lets reverse itpop each element to other stack, let’s say stack2stack2 = [5, 4, 3, 2, 1]It should be clear that popping each element from stack2 and pushing to stack1 will result in the original stack1\. let's use one more stack, say stack3pop each element from stack2 to stack3stack3 = [1, 2, 3, 4, 5]Now popping each element from the stack3 to stack1 will reverse the stack1.
```

所以， ***要用其他栈反转一个栈，我们正好需要 2 个栈。***

这个问题一般在数据结构回合的很多面试中都会被问到。

时间复杂度:O(n) →处理堆栈
空间复杂度:O(n) →存储其他堆栈中的项目

[Github 链接](https://github.com/ajayv1/dsa/blob/main/stack.js)

在 https://weekendtutorial.com/[查看更多这样的文章和教程](https://weekendtutorial.com/)

# 进一步阅读的推荐书籍:

1.  [数据结构和算法变得简单— Narasimha Karumanchi](https://amzn.to/3F6VozP)
2.  [算法介绍— T.H.Cormen](https://amzn.to/3GdjEBr)

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*