# 如何使用新的 Node.js 18 测试运行程序

> 原文：<https://javascript.plainenglish.io/how-to-use-the-new-node-js-18-test-runner-6afaa06e64e0?source=collection_archive---------1----------------------->

## 概述 Node.js 测试模块以及如何使用它为 Node.js 代码编写测试。

![](img/050c4cb57e97aefbccd0070600495a35.png)

Photo by [Antoine Dautry](https://unsplash.com/@antoine1003?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 18 于 4 月 19 日发布，带来了一些新特性。在本文中，我们将介绍实验性的 Node.js 测试模块，以及如何使用它为 Node.js 代码编写测试。

# **我们应该测试什么？**

您可以跟随任何 Node.js 项目，但是为了简单起见，我们将使用在我讨论 Jest 测试的前一篇文章[中使用的相同项目。](/learn-jest-javascript-unit-testing-5ca104b564ce)

[](/learn-jest-javascript-unit-testing-5ca104b564ce) [## 学习 Jest——JavaScript 单元测试

### 单元测试是指测试单个的代码单元，甚至是多个代码单元，以确保它们能正常工作…

javascript.plainenglish.io](/learn-jest-javascript-unit-testing-5ca104b564ce) 

为您的项目创建一个新目录，并创建一个名为`index.js`的新文件:

```
function add(a, b) {
  return a + b
}function subtract(a, b) {
  return a - b
}function multiply(a, b) {
  return a * b
}function divide(a, b) {
  return a / b
}function power(a, b) {
  return a ** b
}module.exports = {
  add,
  subtract,
  multiply,
  divide,
  power
}
```

# **写作测试**

为了在 Node.js 中编写测试，我们使用`[node:test](https://nodejs.org/dist/latest-v18.x/docs/api/test.html)`模块来定义我们的测试，使用`[assert](https://nodejs.org/dist/latest-v18.x/docs/api/assert.html)`模块来做出不同的断言。实际上，我们将使用`[assert/strict](https://nodejs.org/dist/latest-v18.x/docs/api/assert.html)`模块，因为它有一些好处。

首先是它用`===`代替了`==`。在 JavaScript 中，`==`不是严格的相等检查，但`===`是。一个简单的例子:`1 == “1”`为真，`1 === “1”`为假。第二个好处是，当处理对象时，失败的断言将向您显示实际值和期望值的差异，从而更容易检测测试失败的原因。

我们将在名为`test.js`的新文件中创建我们的测试。我们将从我们希望测试的`index.js`中导入测试模块、断言模块和函数。

```
const test = require('node:test')
const assert = require('assert/strict')
const { add, subtract, multiply, divide, power } = require('./index')
// Or for ES6
import test from 'node:test'
import assert from 'assert/strict'
import { add, subtract, multiply, divide, power } from './index'
```

现在，让我们定义我们的第一个测试。我们将断言`add(1, 2)`等于`3`。我们调用`test`方法，并为测试提供一个名称，以及一个运行测试的函数。在函数内部，我们将使用`add`函数和期望值调用`assert`方法。

```
test('add', () => {
  assert.equal(add(1, 2), 3)
})
```

我们可以用`node test.js`运行我们的测试。我们得到一个警告，提醒我们`node:test` runner 是实验性的，将来可能会改变。之后我们的测试运行，我们看到它通过了！

```
(node:8396) ExperimentalWarning: The test runner is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
TAP version 13
ok 1 - add
  ---
  duration_ms: 0.0092444
  ...
1..1
# tests 1
# pass 1
# fail 0
# skipped 0
# todo 0
# duration_ms 0.1194634
```

我想花点时间指出这里使用的格式。在顶部，您可以看到对 TAP 版本 13 的引用。TAP，或 [Test Anything Protocol](https://testanything.org/) ，是一种写测试结果的格式。这是一种以语言无关的方式报告测试结果的标准。这种 TAP 格式可以被测试工具解释，如果需要的话，可以用来创建一个更容易阅读的报告。

[](https://testanything.org/) [## 测试任何协议

### TAP，Test Anything 协议，是测试工具中测试模块之间的一个简单的基于文本的接口。它…

testanything.org](https://testanything.org/) 

如果我们愿意，我们可以为一个功能编写多个测试，组织它们的一个很好的方法是使用子测试。子测试是在作为第一个参数传递给提供给`test`方法的函数的测试上下文中定义的。我们可以用它来为一个函数编写多个边缘案例。如果任何一个子测试失败，整个测试都将失败。我们还应该等待这些方法，否则，测试将在子测试完成之前结束，所有仍在运行的子测试都将被取消。

```
test('subtract', async (t) => {
  await t.test('subtracts two numbers', () => {
    assert.equal(subtract(1, 2), -1)
  }) await t.test('subtracts two numbers', () => {
    assert.equal(subtract(2, 1), 1)
  })
})
```

我将在这里结束它，但是看看您是否可以为剩余的方法编写测试。然后，在你自己的项目中尝试一下！

# **结论**

Node.js 实验测试器是一种很好的编写测试的内置方式。然而，它仍然是实验性的，所以我不推荐在生产项目中使用它，因为 API 可能随时改变。同时，我仍然推荐使用 Jest 或 Mocha 来编写重要项目的测试，但是实验测试器是一个很好的尝试。但前提是你不介意事情有可能会破裂。无论哪种方式，我都推荐学习测试模块，一旦它变得更加稳定，我很乐意在我自己的项目中使用它。尤其是如果有人是 TAP 输出的好消费者。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*