# 如何实现一个完美的 Function.prototype.bind()

> 原文：<https://javascript.plainenglish.io/how-to-implement-a-perfect-function-prototype-bind-56519ebd0e74?source=collection_archive---------12----------------------->

## 通过制作更好的多孔填料来学习

![](img/3c799799eb329fbc382d9ee6a97a4ca1.png)

Photo by [Geometric Photography](https://unsplash.com/@opollophotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，`Function.prototype.bind()`将创建一个绑定到`this`的新函数。我们可以在创建和调用新函数时传递参数。参数序列保持不变。

下面是一个例子:

```
const test = {
  x: 42,
  getX: function () {
    return this.x;
  },
};const unboundGetX = test.getX;
// The function gets invoked at the global scope
console.log(unboundGetX()); // undefinedconst boundGetX = unboundGetX.bind(test);
console.log(boundGetX()); // 42
```

由于不是在严格模式下，默认情况下`this`被替换为`[globalThis](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)`。一旦启用严格模式，`this`将指向`null`或`undefined`。

```
'use strict';const test = {
  x: 42,
  getX: function () {
    return this.x;
  },
};const unboundGetX = test.getX;
// TypeError: Cannot read properties of undefined (reading 'x')
console.log(unboundGetX());
```

除了这些，`bind`返回的新函数也可以作为构造函数实例化一个新对象。

然后将这些特征结合起来，形成一个相对完整的聚合填充:

来分析一下，首先我们得到原函数的`this`和`prototype`，返回一个`boundFunction`。

这个`boundFunction`就是重点。先看它的功能体。我们用`Function.prototype.apply()`的方法来改变调用函数的`this`，其实就是原函数的`this`。

我们用`this instanceof boundFunction ? this : that`作为`apply`指向的`this`，是为了确定`new`当前是否被使用，如果被使用，`this instanceof boundFunction`将返回`true`。

还要注意，我们通过检查它的`prototype`是否是一个对象来确定原始函数是否可以作为一个`constructor`使用。如果是，将返回函数的原型指向由`Object.create(Prototype)`创建的新对象。这样做的原因是为了不丢失`new`上的原始函数原型的属性。

到目前为止，我们编写的 polyfill 已经完成。比较完整，[规范](https://tc39.es/ecma262/#sec-function.prototype.bind)中还有一些复杂的细节没有实现，但是达到了它的教学目的。

希望这有所帮助，感谢阅读！

*不是中等会员？* [*支持我这里*](https://medium.com/@hibrandonevans/membership) *合二为一。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***