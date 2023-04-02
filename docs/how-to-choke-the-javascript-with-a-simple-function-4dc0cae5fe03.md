# 如何用一个简单的函数噎死 JavaScript？

> 原文：<https://javascript.plainenglish.io/how-to-choke-the-javascript-with-a-simple-function-4dc0cae5fe03?source=collection_archive---------13----------------------->

![](img/6906ebfb9452a679f930e93bd167e290.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我发现 JavaScript 函数可能会变慢和阻塞，这促使我探索这个问题。你说的函数扼流圈是什么意思？我是不是不小心写了一个无限循环的算法？不，我没有。我说的是一个基本的函数，但是我需要调用它很多次，比如 10，000 次以上。

先说一个简单的函数？你听说过欧几里德算法吗，就是求两个数的最大公约数的那个？我打赌你有，这是 JavaScript 版本:

```
function **gcd**(a, b) {
  return b == 0 ? a : **gcd**(b, a % b)
}
```

## 用 JavaScript 运行百万次

这个`gcd`函数并不太疯狂，但这正是我想要的，一个基本函数，这样我就可以对它进行一些分析，看看它需要多长时间。我选择了两个大数`461952`和`116298`,这样递归层次就达到了 7 而不是 3。

```
const N = 4000000
console.time('recursion')
for (let i = 0; i < N; i++) { **gcd**(461952,116298) }
console.timeEnd('recursion')
```

我只能运行这个代码不超过 4，000，000 次，然后我的电脑就会死机。实际上，这不是因为溢出，因为我只有 7 级递归。相反，我遇到了内存不足的问题——在这个简单的例子中，它使用了超过 3GB 的内存。这不是很奇怪吗？这么简单的函数怎么会消耗 3GB 的内存呢？我的电脑中病毒了吗？

原来，最后我碰到了一个 v14.17.0 的 node . js bug .`gcd`恰好是一个全局函数。不管是什么原因，当一个函数在全局范围内定义时，它需要在调用时在内存中复制。所以实际上我做了 400 万个函数。为了避免这种情况，我们可以在函数内部定义递归函数，使其成为非全局函数:

```
function gcdWrapper(m, n) {
  function **gcd**(a, b) {
    return (b == 0) ? a : **gcd**(b, a % b)
  } 
  return **gcd**(m, n)
}
```

现在，如果我调用`gcdWrapper`400 万次，它会在 0.2 秒内结束——太神奇了？如果我将 Node.js 切换回 v12.22.1，bug 就会消失。以下是修复后运行该算法的统计数据。

```
 1M    10M   100M     1G     10G
 41ms  366ms   3.6s    36s   6029s  JavaScript
```

统计数据显示 JavaScript 在 100 万到 10 亿之间相当稳定，它随着运行次数的增加而线性增长。对于 10 亿次运行，只需要 36 秒，这还不算太糟糕。但当它达到 100 亿时，似乎开始变得不成比例的缓慢。

## 在铁锈中运行百万次

我也用另一种语言看一下这个算法，做一个比较。我选了 Rust，一种低级语言:

```
fn **gcd**(a: u32, b: u32) -> u32 {
  match b {
    0 => a,
    _ => **gcd**(b, a % b)
  }
}
```

除了类型检查和模式匹配编写，Rust 版本与 JavaScript 版本没有太大区别。我编译它并用`time`运行它，以知道它需要多长时间:

```
rustc -O gcd.rs
time ./gcd
```

以下是统计数据和之前的 JavaScript 数据:

```
 1M    10M   100M     1B     10B  100B
 20ms  100ms  830ms   8.1s     80s  800s  Rust
 41ms  366ms   3.6s    36s   6029s     -  JavaScript
```

Rust 版本也可以线性扩展，尤其是当运行次数超过 1000 万次时。与 JavaScript 版本相比，Rust 版本在不到 10 亿时的运行速度也快了 4 倍。超过 10 亿次运行，Rust 版本变得更快。

# 结论

Node.js 在某些版本中可能会有问题，例如 v14.17.0。当在全局范围内运行大量函数时，如果您使用不稳定版本的 Node.js，它可能会阻塞引擎。在稳定的 Node.js 版本中，例如 v12.22.1，它不会出现这个问题。测试用例显示，在 10 亿次运行的情况下，Node.js 引擎可以非常稳定和线性。超过 10 亿次运行，JavaScript 似乎会大幅减速。请记住，我们在实践中很少能达到这么多的函数调用。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*