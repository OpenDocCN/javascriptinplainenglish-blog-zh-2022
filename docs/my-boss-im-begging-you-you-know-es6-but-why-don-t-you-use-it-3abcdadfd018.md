# 我老板:我求你了😭，你知道 Es6 但是为什么不用？😠

> 原文：<https://javascript.plainenglish.io/my-boss-im-begging-you-you-know-es6-but-why-don-t-you-use-it-3abcdadfd018?source=collection_archive---------1----------------------->

## 老板的 10 条抱怨让我受益匪浅。

![](img/2e8fb3b4742f1e1da2c9873ef1fa0476.png)

# 前言

这就是我的老板在代码评审会议上对团队成员咆哮的方式。原因是他发现项目的许多部分仍然在使用 ES5。不是说 ES5 不好，会有 bug，但是会增加代码量，降低可读性。

碰巧我的老板有代码整洁的习惯。涉及到 3 到 5 年经验的员工，他对这个级别的代码极其不满意，不断抱怨代码。不过我还是觉得从他的抱怨中收获很大，所以决定把老板的抱怨录下来，分享给大家。

# 1.关于提取对象值的投诉

提取属性值在程序中很常见，比如从对象 obj 中获取值。

**老板抱怨**:你为什么不用 ES6 的析构赋值来取值？用 1 行代码做不是更好吗？

**我反对**:我不用 ES6，因为 API 接口属性名不是我想要的。

**老板抱怨**:看来你还没有完全掌握 ES6 的破坏任务。如果要创建的变量名与对象的属性名不一致，可以这样写:

# 2.关于合并数据的投诉

比如合并两个数组或者合并两个对象。

**老板的抱怨**:你是不是忘了 ES6 spread 运算符，合并阵列不考虑重复数据删除？

# 3.关于拼接线的投诉。

**老板投诉**:不如不要像你这样用 ES6 字符串模板。你不知道`${}`里可以做操作？我们可以在`${}`中执行任意的 JavaScript 表达式，执行操作，引用对象属性。

# 4.关于使用 if 的投诉

**老板的抱怨**:我们在 ES6 中使用数组的 includes 方法不是更好吗？

# 5.关于列表搜索的投诉。

在项目中，有些列表的搜索功能是由前端实现的，搜索一般分为精确和模糊两种。一般我们用过滤的方法来实现。

老板的抱怨:你不会使用 ES6 中的 find 方法进行精确搜索吗？你懂性能优化吗？如果在 find 方法中找到符合条件的项，它将不会继续遍历数组。

# 6.对平面阵列的抱怨。

在 JSON 数据中，属性名是部门 id，值是部门雇员的 id 数组。现在我们需要将 department 的所有成员 id 提取到一个数组集合中。

**BOSS 的抱怨**:我需要遍历获取对象的所有属性值吗？你忘了 Object.values 吗？为什么不用 ES6 提供的扁平化方法？

> 备注:使用 Infinity 作为 flat 的参数，所以我们不需要知道 flattened 数组的维数。

# 7.关于获取对象属性值的抱怨。

**老板的抱怨**:你不会在 ES6 中使用可选的链式操作符吗？

# 8.关于添加对象属性的抱怨。

当我们给一个对象添加属性时，如果属性名动态变化，我们该怎么办？

**老板的抱怨**:为什么要多加一个变量？不知道 ES6 中的对象属性名可以用表达式吗？

# 9.对非空判断的抱怨

在处理用户输入时，经常要判断输入框是否已经输入。

**老板的抱怨**:你听说过 ES6 中新的空值合并运算符吗，要写这么多条件吗？

# 10.对异步功能的抱怨

异步函数很常见，并且经常作为承诺来实现。

**老板的抱怨**:你这样用异步函数，不怕形成回调地狱！

# 最后

欢迎你尝试反驳以上 10 条老板投诉。如果你的反驳是合理的，我会在下次代码审查会上为你反驳。

*本文翻译已获原作者(洪陈连新)授权。*

*原地址为*[*https://juejin.cn/post/7016520448204603423*](https://juejin.cn/post/7016520448204603423)

**感谢阅读。**我期待着期待您的关注和阅读更多高质量的文章。

[](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [## 记者:在 JavaScript 中(a==1 && a==2 && a==3)能计算为真吗？

### 是的，这可能是真的，而且有 6 种方式——太神奇了！

javascript.plainenglish.io](/interviewer-can-a-1-a-2-a-3-ever-evaluate-to-true-in-javascript-d2329e693cde) [](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [## “我失去了一个工作机会，只是因为承诺。所有”

### 一次让我好难过的面试经历。

javascript.plainenglish.io](/i-lost-a-job-opportunity-just-because-of-promise-all-be396f6efe87) [](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [## 采访者:“npm 跑 xxx”怎么了？

### 一个大多数人都不知道的秘密。

javascript.plainenglish.io](/interviewer-what-happened-to-npm-run-xxx-cdcb37dbaf44) [](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [## 面试官:可以“x！== x "在 JavaScript 中返回 True？

### 你可能不知道的五个神奇的 JavaScript 知识点！

javascript.plainenglish.io](/interviewer-can-x-x-return-true-in-javascript-7e1d1fa7b5cd) [](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) [## 现在是 2022 年，不要再滥用箭头功能了

### 不应该使用箭头函数的 4 种情况。

javascript.plainenglish.io](/its-2022-don-t-abuse-the-arrow-function-anymore-905862a9c668) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***