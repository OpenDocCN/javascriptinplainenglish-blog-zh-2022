# JavaScript 中迭代数组的最快方法

> 原文：<https://javascript.plainenglish.io/the-quickest-way-to-iterate-over-an-array-in-javascript-db23659b8c24?source=collection_archive---------1----------------------->

## 迭代数组的最有效方法。

现在我们有了一个框架[来测试 JavaScript 代码在不同浏览器上的性能](/using-playwright-and-benchmark-js-to-test-javascript-performance-across-browsers-99fc0dc56e55)，我们可以开始探索可以优化代码的公共领域。一个明显的例子是迭代数组时；做那件事最有效的方法是什么？

![](img/8f5870912513c014c3c1f6dd7ab53a9e.png)

Photo by [Tsvetoslav Hristov](https://unsplash.com/@tsvetoslav?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中有许多不同的原生方法来迭代数组:

*   标准`for`回路
*   `for...in`循环(只要你[不介意顺序](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in#array_iteration_and_for...in)
*   `for...of`循环
*   `Array.prototype.forEach`
*   `while`循环
*   `do...while`循环

此外，其他实用程序库也提供了类似的方法；为了比较，这里我们还将包括来自流行的 [Lodash](https://lodash.com/) 库的`forEach`。

你认为哪个表现最好？你觉得会有区别吗？让我们来看看，通过迭代一个包含 100，000 个数字的数组并对每个数字调用`toString`来进行测试:

结果(对于 2.3GHz i7 MacBook Pro，使用剧作家版本 1.20.2):

```
✓  [chromium] › tests/bench.spec.js:3:1 › Run benchmarks (39s)
Starting benchmark suites...--- iterate --------------------------------------------------------
Running...✅ 'iterate' suite has completed: standard for loop,for...of loop,do...while loop,while loop was the winner! 🏆🏆 standard for loop is fastest (376 ops/sec ±0.81%)
⏳ for...of loop is 0.50% slower (374 ops/sec ±0.91%)
⏳ while loop is 0.92% slower (373 ops/sec ±0.81%)
⏳ do...while loop is 0.93% slower (373 ops/sec ±0.77%)
⏳ _.forEach is 22.88% slower (290 ops/sec ±0.70%)
⏳ ES6 forEach is 24.69% slower (283 ops/sec ±1.32%)
⏳ for...in loop is 69.97% slower (113 ops/sec ±1.36%)✓  [firefox] › tests/bench.spec.js:3:1 › Run benchmarks (41s)
Starting benchmark suites...--- iterate --------------------------------------------------------
Running...✅ 'iterate' suite has completed: standard for loop,while loop was the winner! 🏆🏆 standard for loop is fastest (5566 ops/sec ±0.87%)
⏳ while loop is 0.95% slower (5513 ops/sec ±0.72%)
⏳ do...while loop is 3.67% slower (5362 ops/sec ±0.82%)
⏳ for...of loop is 73.11% slower (1497 ops/sec ±0.52%)
⏳ ES6 forEach is 95.27% slower (263 ops/sec ±1.13%)
⏳ _.forEach is 95.45% slower (253 ops/sec ±0.82%)
⏳ for...in loop is 98.92% slower (60 ops/sec ±1.90%)✓  [webkit] › tests/bench.spec.js:3:1 › Run benchmarks (39s)
Starting benchmark suites...--- iterate --------------------------------------------------------
Running...✅ 'iterate' suite has completed: standard for loop,for...of loop was the winner! 🏆🏆 standard for loop is fastest (281 ops/sec ±0.93%)
⏳ for...of loop is 0.89% slower (278 ops/sec ±0.97%)
⏳ do...while loop is 1.08% slower (278 ops/sec ±0.60%)
⏳ while loop is 1.43% slower (277 ops/sec ±0.61%)
⏳ ES6 forEach is 29.96% slower (197 ops/sec ±0.69%)
⏳ _.forEach is 30.40% slower (195 ops/sec ±0.71%)
⏳ for...in loop is 72.68% slower (77 ops/sec ±1.59%)
```

从这里我们可以看到，在所有的浏览器中，标准的`for`循环、`while`循环和`do...while`循环实际上执行的是相同的，这并不奇怪，因为它们本质上是相同的结构，但是使用了不同的语法。然而，其他选项的表现因浏览器而异，在 Firefox 的 SpiderMonkey 引擎上表现尤为糟糕；在这里，您可能会看到使用标准`for`或`while`循环之外的任何东西都会造成> 70%的性能损失，这是一个显著的差异！同样令人惊讶的是，一个`for...of`循环在 SpiderMonkey 中的表现如此糟糕，尽管它在其他引擎中提供了与`for`和`while`相当的性能。

同样有趣的是`Array.prototype.forEach`函数的性能差异，您可能认为这是标准`for`循环的语法糖，因此性能也一样好，但是尽管这在 WebKit 上似乎是真的，但它在其他引擎上的性能要慢 20–95 %,这一点绝对值得注意。

考虑到 Lodash 在性能方面的知名度，你可能会惊讶地看到它在这里排名垫底。由于 Lodash 是开源的，我们可以看看发生了什么:

[](https://github.com/lodash/lodash/blob/master/.internal/arrayEach.js) [## lodash/arrayEach.js 位于主 lodash/lodash

### 此文件包含双向 Unicode 文本，其解释或编译可能与下面显示的不同…

github.com](https://github.com/lodash/lodash/blob/master/.internal/arrayEach.js) 

Lodash 提供了额外的功能，允许您提前退出迭代，但是对每个循环的额外检查显然会降低它的速度，所以在您不需要它的情况下，您是在做无用功。

总之，如果你关心性能，你应该尽可能坚持使用`for`或`while`循环，但是和以往一样，**只在你需要**时才优化性能；可读性和可维护性通常更重要。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*