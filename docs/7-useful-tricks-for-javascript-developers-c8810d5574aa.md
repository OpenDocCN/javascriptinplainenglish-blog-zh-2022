# JavaScript 开发人员的 7 个有用技巧

> 原文：<https://javascript.plainenglish.io/7-useful-tricks-for-javascript-developers-c8810d5574aa?source=collection_archive---------4----------------------->

## 为开发人员收集了方便的 JavaScript 技巧。

![](img/b8f0412a6db42469a75fe44c9dbb8ab7.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中有许多奇怪的技巧，但我们需要一种经过验证的编程方法。在本文中，我为开发人员总结了 7 个 JavaScript 技巧。如果你觉得不错，请订阅我，我会不断更新更好的文章。

# 提高数字的可读性

为了提高数字的可读性，您可以使用下划线作为分隔符:

# 访问元素的所有自定义数据属性(data-*)

使用`dataset`属性，可以访问元素中的所有自定义数据属性，返回值是一个对象

存在以下 HTML 结构:

当你需要得到`data-id`和`data-user`时，老办法可能是:

上面的方法可以用，但是有点繁琐，我们试着改造一下:

# 析构赋值-数组

与对象析构类似，数组析构更好，因为语义和编程习惯更突出:

正如你所看到的，上面的代码只是假设`res`需要并行处理一个承诺数组来从用户那里拉取一些数据，但糟糕的是只有你知道`res[0]` 是什么意思。

> 你同事:我不知道这是什么意思！

因此，尝试使用更好的语义数组析构技巧:

对了，`[, , otherList]`可以写，但是作为建议，希望你在变量名前面加一个 _ 符号，表示这个变量可能用不到，也是为了 ESLint 检查机制帮助:

# HTML 翻译属性

这是一个可有可无的体验功能，想象一下如果你在做一个技术文档的网站，你希望代码样本中的代码不受系统翻译工具的影响，那么你可以把它添加到父标签或者代码块中。`pre`标签用途:

上述代码块将始终显示您编写的文本，并且不会被翻译成其他语言。

# 快速生成 0–10 的数组

您可能想到的第一件事是使用一个`for`循环来生成一个指定间隔的数组，但是有一种更快更方便的方法

太神奇了！发生了什么，让我解释一下:`Array.keys`返回一个 [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) `[iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator)`，然后可以用它来迭代引用输入源数组中每一项的键。

因此，使用这个特性，我们可以顺序生成 0-10 之间的数字

# 获取数组的最后一个值

嗯，看起来很简单，`arr[arr.length — 1]`会那样做，是的，你是对的，但是这样看起来有点臃肿，有什么办法修改吗？

看起来好多了，但是应该注意这是最新的 ES 建议书(已经是第 4 阶段)，需要添加 polyfill:

# 检查小数是否相等

正如我们知道的 0.1 + 0.2！== 0.3 精度问题，那么这里有一个解决的办法

原因:用户输入的是十进制数，计算机保存的是二进制数。所以计算结果会有偏差，不要直接比较非整数，取上限计算误差。

这个题目到此为止。感谢您的阅读。

# 如需进一步阅读:

[](https://betterprogramming.pub/how-to-write-clean-typescript-code-eda1716eead1) [## 如何编写干净的类型脚本代码

### 掌握如何编写优雅的 TypeScript 代码的 8 个知识点

better 编程. pub](https://betterprogramming.pub/how-to-write-clean-typescript-code-eda1716eead1) [](/7-rare-but-useful-javascript-tricks-cc7f2c380517) [## 7 个罕见但有用的 JavaScript 技巧

### 短小精悍、功能强大的 JavaScript 技巧

javascript.plainenglish.io](/7-rare-but-useful-javascript-tricks-cc7f2c380517) [](https://medium.com/weekly-webtips/improve-your-bad-react-and-typescript-programming-habits-f4a4bf7a9105) [## 改善你的不良反应和打字习惯

### 改掉你不良的编程习惯，做一个自律的人

medium.com](https://medium.com/weekly-webtips/improve-your-bad-react-and-typescript-programming-habits-f4a4bf7a9105) [](/super-useful-typescript-skills-eb35d049fdbd) [## 极其有用的打字和反应技能

### 超级有用的打字和反应技能

javascript.plainenglish.io](/super-useful-typescript-skills-eb35d049fdbd) 

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*