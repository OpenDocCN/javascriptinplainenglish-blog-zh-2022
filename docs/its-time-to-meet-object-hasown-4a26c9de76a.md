# 是时候通过 ES2022 了解 Object.hasOwn()了

> 原文：<https://javascript.plainenglish.io/its-time-to-meet-object-hasown-4a26c9de76a?source=collection_archive---------8----------------------->

## 并向 hasOwnProperty()挥手告别

![](img/3005cc1ec169ce6eea0de3ce25194809.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ES2022 即将推出，随之推出的特性之一是`Object.hasOwn()`。它旨在取代`hasOwnProperty()`方法，并且在 ECMAScript 的新版本之前已经被大多数浏览器支持。要了解它是什么以及它提供的优势，让我们来看看它将取代的方法。

![](img/8602805fad4161ea32deb6316caa2537.png)

JavaScript 使用可以从原型链继承方法的对象，而不是纯粹的类构造。JavaScript 中的大多数对象都是`Object`类的实例，每个实例都有一个到原型对象的链接。历史上，`hasOwnProperty()`一直是检查对象的属性是否被继承的方法。

如果属性是直接的，则`hasOwnProperty()` 方法返回`true`，如果属性是继承的或未声明的，则返回`false`。其实`hasOwnProperty()`是继承了`Object.prototype`的。考虑到上面的例子，让我们来看看它是如何工作的。

这里可以看到原型链的运行，因为`dwyer`从`musician`继承了`sayHello`，两个对象都从`Object`继承了`hasOwnProperty`。这让我们想到了`hasOwnProperty`的一个问题。许多继承的属性可以重新实现，`hasOwnProperty`也不例外。覆盖它会导致麻烦。

使用`Object.create()`创建新对象时，会出现另一个问题。因为该方法接受一个现有对象作为新对象的原型，如果原型为空，它实际上不会继承`hasOwnProperty()`方法。

为了避免这些问题，设置`Object.hasOwn()`代替`hasOwnProperty()`。不受`hasOwnProperty`被改写的影响。

它也可以和`Object.create(null)`一起正常工作，因为它不是一个继承的方法。

准备好和`hasOwnProperty`说再见，因为它很快就会消失在夕阳中。它运行良好，但现在是说再见的时候了。`Object.hasOwn()`已经与大多数浏览器兼容，随着最新 ECMAScript 版本的迅速发布，现在熟悉它是一个好主意。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***