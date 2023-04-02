# 如何在 JavaScript 中求最大公约数

> 原文：<https://javascript.plainenglish.io/how-to-find-the-greatest-common-divisor-in-javascript-c1333aa313db?source=collection_archive---------4----------------------->

## JavaScript 技巧

## JavaScript 中计算 GCD 的不同方法概述

![](img/2e04dbcb32c9a9a75ead187332fce76e.png)

今天的问题与数学有关。具体来说就是求两个正整数的最大公约数。在数学中，两个不都等于零的整数`a`和`b`的最大公约数用`GCD(a,b)`表示，是两者能被除的最大自然数。

# 问题:最大公约数

链接到[形](https://www.codewars.com/kata/5500d54c2ebe0a8e8a0003fd)

求两个正整数的最大公约数。整数可能很大，所以你需要找到一个巧妙的解决方案。

输入`x`和`y`总是大于或等于`1`，因此最大公约数总是大于或等于`1`的整数。

# 解决方案:欧几里德算法

![](img/50db0592699f84c16370ec95704f57e0.png)

原则上，最大公约数可以通过确定两个给定数字的质因数分解并乘以公因数来计算，公因数只考虑一次其最小指数。

这种方法只适用于非常小的数:一个数的素因式分解一般需要太多时间。

欧几里得算法提供了一种更有效的方法。维基百科有一个很好的页面专门介绍[欧几里德算法](https://en.wikipedia.org/wiki/Euclidean_algorithm)，所以我推荐阅读。

总之，有 3 种不同的方法可以得到最大公约数。第一种方法是欧几里得使用的方法，使用减法。

```
function gcd(a, b) {
  while (a !== b) {
    if (a > b) {
      a -= b;
    } else {
      b -= a;
    }
  }
  return a;
}
```

第二种方法使用乘法。

```
function gcd(a, b) {
  while (b !== 0) {
    const t = b;
    b = a % b;
    a = t;
  }
  return a;
}
```

最后，第三种方法是递归函数。

```
const gcd = (x, y) => (y === 0 ? x : gcd(y, x % y));
```

但也有其他方法。

# 最小绝对余数法

![](img/2694db517887b30f8eefb3eb7960a9f3.png)

最小绝对余数法是欧几里得算法的变体，用于寻找两个整数的 GCD。它基于两个整数的 GCD 等于其余数绝对值的 GCD 的观察。当输入整数可能是负数时，这种方法特别有用，因为它确保 GCD 总是正整数。

```
function gcd(a, b) {
  if (a === 0 || b === 0) {
    return Math.max(a, b);
  }
  let r = a % b;
  while (r) {
    a = b;
    b = r;
    r = a % b;
  }
  return Math.abs(b);
}
```

# 二进制 GCD 算法

![](img/f813ccaff7965d6fb333033a3681e9a0.png)

二进制 GCD 算法是欧几里得算法的有效变体，它使用按位操作和递归调用来查找两个整数的 GCD。它的时间复杂度为 O(log n)，其中 n 是两个输入整数中较大的一个，这使得它在某些情况下比其他 GCD 算法更快。但是，由于使用递归调用，它需要更多的内存，并且可能不总是最适合使用的算法。

```
function gcd(a, b) {
  if (a === 0 || b === 0) {
    return Math.max(a, b);
  }
  if (a === b) {
    return a;
  }
  if (a % 2 === 0 && b % 2 === 0) {
    return 2 * gcd(a / 2, b / 2);
  }
  if (a % 2 === 0) {
    return gcd(a / 2, b);
  }
  if (b % 2 === 0) {
    return gcd(a, b / 2);
  }
  return gcd(Math.abs(a - b), Math.min(a, b));
}
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2022 年 12 月 30 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/js-tips-03-greatest-common-divisor/)**。**

## *更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。*

**报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)**

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*