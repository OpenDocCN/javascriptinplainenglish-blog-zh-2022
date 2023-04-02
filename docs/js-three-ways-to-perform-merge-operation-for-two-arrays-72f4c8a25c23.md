# JavaScript 中两个数组的合并操作

> 原文：<https://javascript.plainenglish.io/js-three-ways-to-perform-merge-operation-for-two-arrays-72f4c8a25c23?source=collection_archive---------12----------------------->

## 对两个数组执行合并操作的三种方法

![](img/7fbeba9325ce0fca54a2132d726fc0b8.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文将展示如何使用三种不同的方法合并两个数组。

**1。数组串联方法**

对于大型阵列，建议使用这种方法。

```
const numbers1 = [1, 2, 3];
const numbers2 = [4, 5, 6];
const numbers = numbers1.concat(numbers2);

// numbers:  [ 1, 2, 3, 4, 5, 6 ] 
```

**2。在两个数组上展开运算符**

对于小型阵列，建议使用这种方法。

```
const numbers1 = [1, 2, 3];
const numbers2 = [4, 5, 6];
const numbers = [...numbers1, ...numbers2];

// numbers:  [ 1, 2, 3, 4, 5, 6 ]
```

**3。对于循环按压**

```
const numbers1 = [1, 2, 3];
const numbers2 = [4, 5, 6];
for (let i = 0; i < numbers2.length; i++) {
  numbers1.push(numbers2[i])
}
const numbers = numbers1;

// numbers:  [ 1, 2, 3, 4, 5, 6 ]
```

在结果上，我们可以看到每种方法都有相同的输出。

感谢阅读。

*如果你喜欢这样的故事，想继续看我的故事，请考虑成为* [*中等会员*](https://medium.com/membership) *。每月 5 美元，你可以无限制地访问媒体内容。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)*

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**