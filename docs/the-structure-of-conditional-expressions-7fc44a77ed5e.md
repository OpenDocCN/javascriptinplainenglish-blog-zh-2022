# 条件表达式的结构

> 原文：<https://javascript.plainenglish.io/the-structure-of-conditional-expressions-7fc44a77ed5e?source=collection_archive---------16----------------------->

## 为什么你的应该读起来像自然语言

![](img/069072855c1d2770c78b3cda66c79852.png)

Photo by [Clarissa Watson](https://unsplash.com/@clarephotolover?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当谈到干净的代码时，有一些事情是大多数程序员都会注意的。命名事物或者使用短函数体就是两个例子。但是还有其他更微妙的代码味道会让你的代码难以理解。我最近在一次代码审查中偶然发现的一件事是条件逻辑的结构。看看下面的 JavaScript 代码片段。你能立即知道输出是什么吗？

```
const array = [1, 2, 3];if (0 < array.length) {
  console.log('The array has values');
} else {
  console.log('The array is empty');
}
```

这不是一个棘手的问题，您可能已经正确地观察到代码将打印出*“数组有值”*。但是需要多少认知努力呢？你可能至少要看两遍代码。

这是同样的东西，但是不一样。

```
const array = [1, 2, 3];if (array.length > 0) {
  console.log('The array has values');
} else {
  console.log('The array is empty');
}
```

简单多了，对吧？

想象一下，必须向另一个人解释其中的逻辑。你可能会以类似于*的话开始:“当数组长度大于零时，输出是‘数组有值’。”*

你不会说的是*“当零小于数组长度时，输出是‘数组有值’。”*

这里感兴趣的是数组长度，所以它应该是句子的主语。在第二个例子中，主语是倒置的，类似于`0 === array.length`表达式。语法是正确的，但是语义模糊不清。你的大脑不习惯这样，当它偶然发现时就会出错。然后，它必须进行另一次往返来理解表达式。这说明了本文的结论:**条件表达式应该像自然语言一样结构化。**

你的头脑被训练去理解自然语言。类似地组织你的代码将会使它更容易阅读和理解。这是一个微妙的变化，但当代码变得更加复杂时，它会产生巨大的影响。下次编写条件表达式时，请记住这一点。

*原载于 2022 年 3 月 8 日*[*https://stricker . digital*](https://stricker.digital/posts/the-structure-of-conditional-expressions/)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*