# 就因为斐波那契，我失去了一个工作机会

> 原文：<https://javascript.plainenglish.io/i-lost-a-job-opportunity-just-because-of-fibonacci-cd26a6467ec1?source=collection_archive---------2----------------------->

## 一次让我好难过的面试经历。

![](img/c9ef7ca4dc3fcebd323fb59fae85a842.png)

这是不久前发生在我朋友身上的一次面试经历。面试官希望他实现斐波那契函数。可惜我朋友现场发挥不好，回答不了问题。

面试结束后，面试官粗鲁地说，**“你的 JavaScript 基础不够扎实，对很多 JavaScript 原理了解不够。”**

实际上，我对面试官的这种行为感到困惑。无法实现斐波那契是否意味着基础没有掌握？很奇怪，你不觉得吗？

在接下来的内容中，我试图揭开斐波纳契方法的神秘面纱。所以让我们开始吧。

# 问题描述

让我们看看这是一个什么样的问题，我的朋友们！！！

(来自[leetcode.com](https://leetcode.com/problems/fibonacci-number/)

通常表示为 F(n)的斐波纳契数列形成了一个序列，称为斐波纳契数列，每个数字都是前面两个数字的和，从 0 和 1 开始。也就是说，

```
F(0) = 0, F(1) = 1
// !!! Please note this formula
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

给定 n，计算 F(n)。

示例 1:

```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

示例 2:

```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

示例 3:

```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

限制

0 <= n <= 30

# 1\. Solution 1

Please let’s catch these highlights below.

```
F(0) = 0, F(1) = 1
// !!! Please note this formula
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

I’m sure you’ll soon be able to write a first solution that uses loops to solve this problem.

```
const fibonacci = (n) => {
  let a = 1
  let b = 0
  let t

  while (n > 0){
    t = a
    a = a + b
    b = t
    n--
  }

  return b
}
```

**有测试**

太好了，所有的测试结果都如我们所料。

```
fibonacci(0) // 0
fibonacci(1) // 1
fibonacci(2) // 1
fibonacci(3) // 2
fibonacci(4) // 3
```

但我认为面试官对结果不满意，让我们试试新的解决方案。

# 2.#解决方案 2

```
F(0) = 0, F(1) = 1
// !!! Please note this formula
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

请让我们再回顾一下这个问题。你找到了吗？它完全符合递归函数的特点，所以我们很容易写出新的答案。

```
const fibonacci = (n) => {
  if (n === 0) {
    return 0
  }

  if (n === 1 || n === 2) {
    return 1
  }

  return fibonacci(n -2) + fibonacci(n - 1)
}
```

**有测试**

与解决方案 1 一样，我们也得到了正确的结果。

```
fibonacci(0) // 0
fibonacci(1) // 1
fibonacci(2) // 1
fibonacci(3) // 2
fibonacci(4) // 3
```

**等等，让我们暂时停止前进，我总觉得它有什么缺陷。**

请让我们试着推导出`fibonacci(10)`的计算。

```
// fibonacci(10)
10 => 9 + 8 // We need to calculate the results of 9 and 8
9 => 8 + 7 // We need to calculate the results of 8 and 7
8 => 7 + 6 // We need to calculate the results of 7 and 6
7 => 6 + 5 // We need to calculate the results of 6 and 5
6 => 5 + 4 // We need to calculate the results of 5 and 4
5 => 4 + 3 // We need to calculate the results of 4 and 3
4 => 3 + 2 // We need to calculate the results of 3 and 2
2 => 1 + 0 //We need to calculate the results of 1 and 0
1 => 1 // We need to calculate the results of 1
0 => 0 // We need to calculate the results of 0
```

我可能知道是什么问题，`fibonacci(10)`他做了很多重复计算。比如`fibonacci(8)`、`fibonacci(7)`、`fibonacci(6)`的双重计算...

如果我们缓存`fibonacci(n)`的每一次计算结果，会更快吧？

```
let count2 = 0
const fibonacci2 = (n) => {
  // The result has already been calculated, just return the result directly
  if (typeof fibonacci2[ n ] !== 'undefined') {
    return fibonacci2[ n ]
  }

  count2 += 1

  if (n === 0) {
    return 0
  }
  if (n === 1 || n === 2) {
    return 1
  }
  const res = fibonacci2(n -2) + fibonacci2(n - 1)
  // Cache the results of the calculation
  fibonacci2[ n ] = res
  return res
}

console.log(fibonacci2(40)) // 102334155
console.log(count2) // 41 fibonacci2 obtained the result after only 41 calculations
```

你永远也猜不到`fibonacci`函数要计算多少次才能得到结果。

```
let count1 = 1

const fibonacci = (n) => {
  count1 += 1

  if (n === 0) {
    return 0
  }

  if (n === 1 || n === 2) {
    return 1
  }

  return fibonacci(n -2) + fibonacci(n - 1)
}

console.log(fibonacci(40)) // 102334155
console.log(count1) // 204668310 The fibonacci was surprisingly calculated 204668310 times.
```

**天啊！我终于知道为什么我的朋友失去了这个工作机会。面试官希望她不仅要追求答案，还要知道如何优化答案。**

# 最后

**感谢阅读。**我期待期待您的关注和阅读更多高质量的文章。

[](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/my-boss-you-dont-know-react-at-all-f493970f1807) [## 我老板:你根本不知道反应！😠

### 你必须知道的 React 的 3 种错误用法。

javascript.plainenglish.io](/my-boss-you-dont-know-react-at-all-f493970f1807) [](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [## 让你看起来像高级开发人员的 8 个很酷的 GitHub 技巧

### 使用 GitHub 可以做的 8 件很酷的事情

javascript.plainenglish.io](/8-cool-github-tricks-to-make-you-look-like-a-senior-developer-ab8fe9ae9b14) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/what-does-123-tostring-length-123-print-out-in-javascript-2c804a414325) [## 123['toString']。length + 123)用 JavaScript 打印出来？

### 95%的前端开发者回答错误的问题。

javascript.plainenglish.io](/what-does-123-tostring-length-123-print-out-in-javascript-2c804a414325) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*