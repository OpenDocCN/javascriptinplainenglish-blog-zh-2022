# 如何在 JavaScript 中深度克隆一个对象

> 原文：<https://javascript.plainenglish.io/how-to-deep-clone-an-object-in-javascript-92ec95e66490?source=collection_archive---------16----------------------->

![](img/0fd21101df1367c392614033a0c303b1.png)

Photo by [Phil Shaw](https://unsplash.com/@phillshaw?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有几种方法可以在 JavaScript 中深度克隆对象:

1.  `JSON.parse()`和`JSON.stringify()`方法:该方法涉及使用`JSON.stringify()`将对象序列化为 JSON 字符串，然后使用`JSON.parse()`将其反序列化回对象。这里有一个例子:

```
const originalObject = {
  a: 1,
  b: {
    c: 2,
    d: 3
  }
};
const clonedObject = JSON.parse(JSON.stringify(originalObject));
```

2.`Object.assign()`方法:该方法包括创建一个新对象，并使用`Object.assign()`方法将属性从原始对象复制到新对象。这里有一个例子:

```
const originalObject = {
  a: 1,
  b: {
    c: 2,
    d: 3
  }
};
const clonedObject = Object.assign({}, originalObject);
```

3.`spread operator` : **如果数据没有嵌套**，则 spread 运算符会对数据进行深度复制。当数组或对象中有嵌套数据时，spread 运算符将创建最顶层数据的深层副本和嵌套数据的浅层副本。所以，如果你的数据不是嵌套的，你可以使用 spread 运算符来深度克隆一个对象。

```
const originalObject = {
  a: 1,
  b: 2
};
const clonedObject = { ...originalObject };
```

4.`lodash`库:这个方法包括使用`lodash`库中的`_.cloneDeep()`函数来深度克隆对象。这里有一个例子:

```
const _ = require('lodash');
const originalObject = {
  a: 1,
  b: {
    c: 2,
    d: 3
  }
};
const clonedObject = _.cloneDeep(originalObject);
```

总之，有几种方法可以在 JavaScript 中深度克隆一个对象，包括使用`JSON.parse()`和`JSON.stringify()`、`Object.assign()`、spread 操作符和`lodash`库。最适合您的方法将取决于您的具体需求和要求。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*